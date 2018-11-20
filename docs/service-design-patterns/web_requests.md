# Handling Web Requests
It is easy to build an HTTP endpoint using nio blocks, and in fact an entire API can be constructed starting with the _WebHandler_ family of blocks. Every HTTP endpoint created will use a Handler block to receive requests, and an Output block to dispatch a response. Furthermore there are two distinct types of each block, "regular" and JSON, where the former is usually used for plain text and web pages, and the latter for structured data.

---

Every web request is made from a *client* to a *server*, which in this case is a [_WebHandler_](https://blocks.n.io/WebHandler) or [_WebJSONHandler_](https://blocks.n.io/WebJSONHandler) block. For more information on which to use, see the individual block documentation, this guide applies to either although the signal structure may vary. Every request generally expects a response, which is provided by the [_WebOutput_](https://blocks.n.io/Weboutput) and [_WebJSONOutput_](https://blocks.n.io/WebJSONOutput) blocks:
```
+----------------------------------+
| WebHandler                       |
|   Endpoint: web_test             |
|   Port: 8182                     |
|   Require Authentication: False  |
|                                  |
+-----------------O----------------+
                  |
                  |
                  V
+-----------------O----------------+
| WebOutput                        |
|   Response Body: Hello, world!   |
|   Response Status: 200           |
|                                  |
+----------------------------------+
```
If running this example on `localhost`, one can visit `http://localhost:8182/web_test` in any web browser and see `Hello, world!` on a plain web page. SSL encryption of this endpoint uses the same configuration as the running nio instance. If **Require Authentication** is True, clients must include an `authorization` header in requests. For more information on using SSL in your instance please see [the docs](https://docs.n.io/running-nio/ssl.html).

Included in the signal emitted by the _WebHandler_ is a new attribute *id*, which is used by the _WebOutput_ block's **RequestID** to send the response to the correct client and close the socket. Without a valid **RequestID** the _WebOutput_ will fail to build a response.

This example shows how to create a web service that returns the last temperature streamed from a specified freezer. Clients must include a "freezer" parameter in their request (such as `<host>:8182/get_temp?freezer=1`) which is used by the [_MergeStreams_](https://blocks.n.io/MergeStreams) block to get the matching temperature value from a stream of signals:
```
          +--------------------------+
          | WebHandler               |
          |  Endpoint: get_temp      |           {"freezer": "1", "temp_C": -1.0}
          |  Host: 0.0.0.0           |           {"freezer": "2", "temp_C": -2.0}
          |  Port: 8182              |            ...
          +--------------O-----------+                           |
                         |                                       |
                         |                                       |
                         V                                       |
+------------------------O----------------------+                |
| Modifier                                      |                |
|   Exclude Existing Fields: False              |                |
|   Fields:                                     |                |
|     Attribute Name: freezer                   |                |
|     Attribute Value: {{ $params["freezer"] }} |                |
+------------------------O----------------------+                |
                         |                                       |
                         +---------+        +--------------------+
                                   |        |
                                   V        V
                      +------------O--------O------------+
                      | MergeStreams                     |
                      |  Group By: {{ $freezer }}        |
                      |  Notify Once: False              |
                      |                                  |
                      +-----------------O----------------+
                                        |
                                        |
                                        V
                      +-----------------O----------------+
                      | WebOutput                        |
                      |  Response Body: {{ $temp_C }}    |
                      |  Response Status: 200            |
                      |                                  |
                      +----------------------------------+
```
## The More You Know:
The parameters included with a web request will always be strings, even if representing an integer. It's important that these datatypes match if used in a **Group By** expression, for simplicity this example assumes the values of `freezer` are strings. For more information see the standard [Built-in Types](https://docs.python.org/3/library/stdtypes.html).
