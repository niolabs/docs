# Industrial Protocols: Ethernet/IP
Able to communicate with any device that implements [Ethernet/IP](https://www.odva.org/Technology-Standards/EtherNet-IP/Overview) Explicit Messaging, these blocks are useful for connecting to automation equipment and controllers and other generic CIP devices.

---

## Unpacking Binary Data From a Device
For every signal processed, both the [_EIPGetAttribute_](https://blocks.n.io/EIPGetAttribute) and [_EIPSetAttribute_](https://blocks.n.io/EIPSetAttribute) blocks will execute a single request to a target device, and emit a signal containing the results of that request. The path of CIP objects and the attributes available is defined by the target device manufacturer. In the case of *getting* an attribute, the outgoing signal will contain the configured `host` and object `path`, and most importantly a `value` attribute that contains some raw bytes like `{"value": b"\xbf\x80\x00\x00"}`. Generally the easiest way to deal with this binary data is to use an [_UnpackBytes_](https://blocks.n.io/UnpackBytes) block to build a real number. The method of interpretation for this data is provided by the device vendor, and a **New Signal Attrbute** configured following that method:
```
                      ...
                       |
                       |
                       V
+----------------------O--------------------+
| EIPGetAttribute                           |
|   Hostname: <host>                        |
|   Class ID: <id>                          |
|   Instance: <inst>                        |
|   Attribute: <attr>                       |
+----------------------O--------------------+
                       |
                       |
                       V
+----------------------O--------------------+
| UnpackBytes                               |
|   New Signal Attributes:                  |
|     New Attribute Key: {{ $host }}_temp_C |
|     Bytes To Unpack: {{ $value }}         |
|     Format: float                         |
|     Endian: big                           |
|   Exclude Existing Fields: True           |
+----------------------O--------------------+
                       |
                       |
                       V
            {"<host>_temp_C": -1.0}
```
If for example the device manual specifies that this is an [IEEE 754](https://en.wikipedia.org/wiki/IEEE_754) floating point number (big endian) the value ultimately decodes to `-1.0`. The precision of this float is inferred from the number of bytes to unpack and does not need to be configured. By selecting **Exclude Existing Fields** the final signal in this diagram contains only the unpacked vale in the new attribute(s) configured.

*Setting* an attribute is very similar, using [_PackBytes_](https://blocks.n.io/PackBytes) to store an integer or float into the specified number of bytes (therefore defining the range of integers, or precision of floats).

To interact with an Allen-Bradley CongtrolLogix or CompactLogix controller, see the [_ReadTag_](https://blocks.n.io/ReadTag) and [_WriteTag_](https://blocks.n.io/WriteTag) blocks specific for those devices.
