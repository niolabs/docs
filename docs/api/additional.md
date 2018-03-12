# Additional APIs

The nio Platform has additional APIs that you may find useful as you explore what nio has to offer.

---

## Configuration refresh API

The `/config/refresh` endpoint, provided by the `config` component, is used to update a running nio instance when its block or service configuration files were modified through some means other than the `/blocks` and `/services` APIs. For example, if you use a text editor to modify a block configuration file, you need to tell the running nio instance to use those changes. You can do this with a GET request to the `/config/refresh` endpoint of your running instance.

    curl -XGET 'localhost:8181/config/refresh' --user 'Admin:Admin'

## Log API

The `/log` endpoint, provided by the `log_api` component, can be used to retrieve logs and modify the log levels of an instance's components and services.

To view an intstance's loggers, use a GET request to `log`. To retrieve all the loggers and the associated log levels send a GET request to `/log?level`.

To retrieve the log entries of a component or service, use a GET request to the `/log/entries` endpoint.
The optional URL parameters are `name` (service name), `level`, `component`, and `count`.

Sample log entry requests:
```
- read last 100 entries from main (core process)
    curl -XGET 'localhost:8181/log/entries' --user 'Admin:Admin'
- read last 100 entries at ERROR level from main (core process)
    curl -XGET 'localhost:8181/log/entries?component=main&level=ERROR' --user 'Admin:Admin'
- read last 20 entries at ERROR level from service1
    curl -XGET 'localhost:8181/log/entries?name=service1&level=ERROR&count=20' --user 'Admin:Admin'
- read last 100 entries at WARNING level for service 'service1'
    curl -XGET 'localhost:8181/log/entries?name=service1&level=WARNING' --user 'Admin:Admin'
- read last 100 entries for component 'main.BlockManager'
    curl -XGET 'localhost:8181/log/entries?component=main.BlockManager' --user 'Admin:Admin'
```

To change the log level of a specific logger, send a POST request to `/log` with a JSON body containing
```
{
    "log_level": "<INFO/DEBUG/WARNING/ERROR>",
    "logger_name": "<name of logger to change level>"
}
```

You can also send GET/POST requests to read and modify service-specific logs.  This is done using the `/log/service/<service_name>` endpoint.  
The service will need to be running and started for the endpoint to work.
The service-specific endpoint will not return log entries but the request
```
curl -XGET 'localhost:8181/log/service/service1?level' --user 'Admin:Admin'
```
will return all the loggers and associated levels for the service1 service.  Use the same JSON body above to modify the log levels.
