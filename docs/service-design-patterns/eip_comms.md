# Industrial Protocols: Ethernet/IP
Able to communicate with any device that implements CIP Explicit Messaging, these blocks are useful for connecting to automation equipment and controllers.

---

## Unpacking Binary Data From a Device
For every signal processed, both the _EIPGetAttribute_ and _EIPSetAttribute_ blocks will execute a single request to a target device, and emit a signal containing the results of that request. The indexing of CIP objects and the attributes available is defined by the target device manufacturer. In the case of *getting* an attribute, the outgoing signal will contain the requested value as raw binary data, and the parsing or interpretation of that data is defined by the device vendor. Using the information provided by the manual we can use _UnpackBytes_ to build a real number:

```
                     ...

                      |
                      |
                      V
+---------------------O-------------------+
| EIPGetAttribute                         |
|   Hostname: <ipaddr>                    |
|   ...                                   |
|                                         |
+---------------------O-------------------+
                      |
                      |
                      V
+---------------------O-------------------+
| UnpackBytes                             |
|   New Signal Attributes:                |
|     New Attribute Key: temp_C           |
|     Bytes To Unpack: {{ $value }}       |
|     Format: float                       |
|     Endian: big                         |
|   Exclude Existing Fields: True         |
|                                         |
+---------------------O-------------------+
                      |
                      |
                      V

              {"temp_C": -1.0}
```
For every signal processed by _EIPGetAttribute_ a signal will be emitted that contains the host and object path information, and most importantly a `value` attribute that contains some raw bytes like `{"value": b"\xbf\x80\x00\x00"}`, and the manual specifies that this is an IEEE-754 floating point number (big endian) so it decodes to `-1.0`.

*Setting* an attribute is very similar, using _PackBytes_ to store an integer or float into the specified number of bytes (i.e. precision). To interact with an Allen-Bradley CongtrolLogix or CompactLogix controller, see the [ReadTag](https://blocks.n.io/ReadTag) and [WriteTag](https://blocks.n.io/WriteTag) blocks specific for those devices.
