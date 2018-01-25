# Services API

Services are the real-time processes that run on a nio instance where you configure the logic of the workflow of blocks to make interesting things happen. Information about and interaction with the services of a running nio instance are available through the `/services` API.

---

## Get API

The Get API returns a JSON body with information about a service based on its name. The following example gets the information for the service **SimulateAndLog**.

    curl -XGET 'http://localhost:8181/services/SimulateAndLog'

The result of the previous request is

```json
{
  "type": "Service",
  "version": "1.0.0",
  "name": "SimulateAndLog",
  "log_level": "NOTSET",
  "auto_start": false,
  "status": "stopped",
  "execution": [
    {
      "name": "Simulate",
      "receivers": {
        "__default_terminal_value": [
          {
            "name": "Log",
            "input": "__default_terminal_value"
          }
        ]
      }
    },
    {
      "name": "Log",
      "receivers": []
    }
  ],
  "mappings": [],
  "sys_metadata": "{\"Simulate\":{\"locX\":248,\"locY\":102},\"Log\":{\"locX\":202,\"locY\":210}}"
}
```

  **type**<br>The service type of the service configuration. Usually, the type is `Service`.

  **version**<br>The version of the service type when the service configuration was created.

  **name**<br>The name of the service configuration. This must be unique among all services in the instance.

  **log_level**<br>The number of log messages displayed, from `NOTSET` on the bottom, which includes all messages logged, through `DEBUG`, `INFO`, `WARNING`, and `ERROR`, to `CRITICAL` on the top, which contains only the most critical messages. Messages are shown for the specified **log_level** and all levels above.

  **auto_start**<br>A boolean that indicates if the service will start when the nio Platform starts up.

  **status**<br>Current status of the service: configuring, configured, starting, started, stopping, stopped, and error.

  **execution**<br>The configuration of inter-block connections in the service. Block connections are defined as a list of dictionaries that specify a block **name** and the blocks it sends signals to, called **receivers**. The **receivers** specify the output terminal in the source block that emits signals and the input terminal in the receiver block that receives signals.

  **mappings**<br>The local ID of a block configuration. If a single block configuration is used multiple times in a service, a new local name is created for each additional use of that block, and those new names are specified in mappings.

  **sys_metadata**<br>Data that is used by the nio System Designer to store block locations on the canvas.

---

## Get all API

In addition to getting the details of one service configuration, specified by name, you can get the details of all service configurations in one request.

    curl -XGET 'http://localhost:8181/services'

---

## Create API

If you're working with a nio project from scratch, you need to create and configure services. Create a new service with the Create API by sending a POST request with the applicable JSON data. When creating a new service, you can optionally include the configured values of the service type properties. At a minimum, you must specify the service **type** and **name** and any configuration values for required service properties that do not have a default value. The following example creates a **SimulateAndLog** service of the basic type `Service`.

    curl -XPOST 'http://localhost:8181/services' --data '{"type": "Service", "name": "SimulateAndLog"}' -H 'Content-Type: applcation/json'

---

## Update API

When you want to update the configuration of a service, send a PUT request to `/services` with the service name as the endpoint and include any new JSON data. You only need to include the properties that you are updating in your PUT request, in this case, **log_level**.

    curl -XPUT 'http://localhost:8181/services/SimulateAndLog' --data '{"log_level": "DEBUG"}' -H 'Content-Type: applcation/json'

---

## Delete API

To delete a service, send a DELETE request to `/services` with the name of the service you want to delete as the endpoint.

    curl -XDELETE 'http://localhost:8181/services/SimulateAndLog'
