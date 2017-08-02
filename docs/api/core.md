# Core APIs

{{ book.product }} core has a few crucial API endpoints: `/nio` and `/shutdown`.

## nio

The `/nio` endpoint is where you will find information about your running {{ book.product }} instances:

    curl -XGET 'localhost:8181/nio' -H 'authorization: Basic <your encrypted password>'

The following JSON body is returned

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

**components**<br>Core [components](../components/README.md) running in the binary.

**modules**<br>Modules that interface between the core and blocks such as Communication and Persistence.

**nio**
  - **binary**<br>Name of executable binary that was run against the project.
  - **build**<br>Build version of binary.
  - **version**<br>Version of {{ book.product }} framework, not to be confused with `build` which is the version of the `binary`.

**start_time**<br>Datetime string at which {{ book.product }} was started.


## Shutdown

The `/shutdown` endpoint is used to shutdown a running {{ book.product }} instance.

    curl -X GET 'http://localhost:8181/shutdown' -H 'authorization: Basic QWRtaW46QWRtaW4='

The following HTML is returned after a successful shutdown request

    Shutdown complete
