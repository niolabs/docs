# Core APIs

{{ book.product }} core has a few crucial API endpoints: `/nio` and `/shutdown`.  

## nio

The `/nio` endpoint is used to find information, such as versioning, about your running {{ book.product }} instances 

    curl -XGET 'localhost:8181/nio'

The following JSON body is returned:

```json
{
    "components": {
        "ServiceMonitor": {},
        "ConfigMonitor": {},
        "ProjectManager": {},
        "LogManager": {},
        "BlockManager": {},
        "ManagementPublisher": {},
        "RESTManager": {},
        "ServiceManager": {},
        "ZmqCommunicationAPIManager": {}
    },
    "modules": {},
    "nio": {
        "version": "2.1.0",
        "binary": "nio_full",
        "build": "20170509"
    },
    "start_time": "2017-08-02 11:24:19.427352"
}
```

**components**<br>The core [components](../components/README.md) running in the binary.

**modules**<br>The modules that interface between the core and blocks, such as Communication and Persistence.

**nio**
  - **binary**<br>The name of the executable binary that was run against the project.
  - **build**<br>The build version of the binary.
  - **version**<br>The version of the {{ book.product }} framework (not the version of the **binary**).

**start_time**<br>A datetime string that indicates when {{ book.product }} was started.


## Shutdown

The `/shutdown` endpoint is used to shutdown a running {{ book.product }} instance.

    curl -XGET 'http://localhost:8181/shutdown'

The following HTML is returned after a successful shutdown request:

    Shutdown complete
[](fake comment)