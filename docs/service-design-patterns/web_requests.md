# Handling Web Requests
It is easy to build an HTTP endpoint using nio blocks, and in fact an entire API can be constructed starting with the _WebHandler_ family of blocks. There are two distinct types of each block, "regular" and JSON, where the former is usually used for plain text and the latter for structured data, such as that returned by a RESTful API.

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
|   Response Body: hello world     |
|   Response Status: 200           |
|                                  |
+----------------------------------+
```
Included in the signal emitted by the _WebHandler_ is a new attribute *id*, which is used by the _WebOutput_ block's **RequestID** to send the response to the correct client and close the socket. Without a valid **RequestID** the _WebOutput_ will fail to build a response.

This example shows how to serve the most current signal in a stream to clients. The _Modifier_ block is putting an entire incoming signal inside a single attribute, `body`, by calling the `to_dict` method. If a client makes a GET request to `<host>:8182/temps` a 200 status will be returned along with the string representation of the input signal that was stored in `body`:
```
                              {freezer_1: -1.0, freezer_2: -2.0, ... }

                                                  |
                                                  |
                                                  V
+-----------------------+    +--------------------O-------------------+
| WebHandler            |    | Modifier                               |
|   Endpoint: temps     |    |   Fields:                              |
|   Port: 8182          |    |     Attribute Name: body               |
|                       |    |     Attribute Value: {{ $.to_dict() }} |
+-----------O-----------+    +--------------------O-------------------+
            |                                     |
            +---------+        +------------------+
                      |        |
                      V        V
           +----------O--------O----------+
           |  MergeStreams                |
           |    Notify Once: False        |
           |                              |
           |                              |
           +---------------O--------------+
                           |
                           |
                           V
           +---------------O--------------+
           | WebOutput                    |
           |   Response Body: {{ $body }} |
           |   Response Status: 200       |
           |                              |
           +------------------------------+

```
This final example shows how to parse the request parameters to serve only the data requested. Clients must include a "freezer" parameter in their request, which is used by the _MergeStreams_ block to get the matching temperature value:
```
             +-----------------------+
             | WebHandler            |
             |   Endpoint: get_temp  |
             |   Port: 8182          |           {"freezer": 1, "temp_C": -1.0}
             |                       |           {"freezer": 2, "temp_C": -2.0}
             +-----------O-----------+             ...
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
                       +-----------O--------O-----------+
                       | MergeStreams                   |
                       |   Group By: {{ $freezer }}     |
                       |   Notify Once: False           |
                       |                                |
                       +----------------O---------------+
                                        |
                                        |
                                        V
                       +----------------O---------------+
                       | WebOutput                      |
                       |   Response Body: {{ $temp_C }} |
                       |   Response Status: 200         |
                       |                                |
                       +--------------------------------+
```