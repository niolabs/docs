# Handling Web Requests
It is easy to build an HTTP endpoint using nio blocks, and in fact an entire API can be constructed starting with the _WebHandler_ family of blocks. Every HTTP endpoint created will use a Handler block to receive requests, and an Output block to dispatch a response. Furthermore there are two distinct types of each block, "regular" and JSON, where the former is usually used for plain text and websites, and the latter for structured data.

---

Every web request is made from a *client* to a *server*, which in this case is a _WebHandler_ or _WebJSONHandler_ block. For more information on which to use, see the individual block documentation, this guide applies to either. Every request generally expects a response, which is provided by the _WebOutput_ and _WebJSONOutput_ blocks:
```
+----------------------------------+
| WebHandler                       |
|   Endpoint: web_test             |
|   Port: 8182                     |
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
Included in the signal emitted by the _WebHandler_ is a new attribute *id*, which is used by the _WebOutput_ block's **RequestID** to send the response to the correct client and close the socket. Without a valid **RequestID** the _WebOutput_ will fail to build a response.

This example shows how to create a web service that returns the last temperature streamed from a specified freezer. Clients must include a "freezer" parameter in their request (such as `<host>:8182/get_temp?freezer=1`) which is used by the _MergeStreams_ block to get the matching temperature value from a stream of signals:
```
          +--------------------------+
          | WebHandler               |
          |  Endpoint: get_temp      |
          |  Port: 8182              |           {"freezer": 1, "temp_C": -1.0}
          |                          |           {"freezer": 2, "temp_C": -2.0}
          +--------------O-----------+             ...
                         |                                      +
                         |                                      |
                         V                                      |
+------------------------O----------------------+               |
| Modifier                                      |               |
|   Exclude Existing Fields: False              |               |
|   Fields:                                     |               |
|     Attribute Name: freezer                   |               |
|     Attribute Value: {{ $params["freezer"] }} |               |
+------------------------O----------------------+               |
                         |                                      |
                         +---------+        +-------------------+
                                   |        |
                                   V        V
                      +------------O--------O------------+
                      | MergeStreams                     |
                      |  Group By: {{ str($freezer) }}   |
                      |  Notify Once: False              |
                      |                                  |
                      +-----------------O----------------+
                                        |
                                        |
                                        V
                      +----------------O-----------------+
                      | WebOutput                        |
                      |  Response Body: {{ $temp_C }}    |
                      |  Response Status: 200            |
                      |                                  |
                      +----------------------------------+
```
