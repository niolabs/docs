# Services types API

Service types contain metadata for nio services and can be accessed with `/services_types` API.

---

## Get API

The Get API returns a JSON body with information about the service type with a particular name. For example, send a GET request to `/services_types` with the name `Service` as its endpoint

    curl -XGET 'http://localhost:8181/services_types/Service'

and the result will be

```json
{
  "Service": {
    "name": "Service",
    "properties": {
      "name": {
        "default": null,
        "allow_none": false,
        "type": "StringType",
        "title": "Name",
        "visible": true
      },
      "mappings": {
        "obj_type": "BlockMapping",
        "list_obj_type": "ObjectType",
        "visible": true,
        "default": [],
        "allow_none": false,
        "type": "ListType",
        "title": "Mappings",
        "template": {
          "name": {
            "default": null,
            "allow_none": false,
            "type": "StringType",
            "title": "Name",
            "visible": true
          },
          "mapping": {
            "default": null,
            "allow_none": false,
            "type": "StringType",
            "title": "Mapping",
            "visible": true
          }
        }
      },
      "auto_start": {
          "default": true,
          "allow_none": false,
          "type": "BoolType",
          "title": "Auto Start",
          "visible": true
      },
      "sys_metadata": {
          "default": "",
          "allow_none": false,
          "type": "StringType",
          "title": "Metadata",
          "visible": true
      },
      "log_level": {
        "options": {
          "CRITICAL": 50,
          "DEBUG": 10,
          "INFO": 20,
          "WARNING": 30,
          "NOTSET": 0,
          "ERROR": 40
        },
        "visible": true,
        "default": "NOTSET",
        "allow_none": false,
        "type": "SelectType",
        "title": "Log Level",
        "enum": "LogLevel"
      },
      "execution": {
        "obj_type": "BlockExecution",
        "list_obj_type": "ObjectType",
        "visible": true,
        "default": [],
        "allow_none": false,
        "type": "ListType",
        "title": "Execution",
        "template": {
          "name": {
            "default": null,
            "allow_none": false,
            "type": "StringType",
            "title": "Name",
            "visible": true
          },
          "receivers": {
            "default": null,
            "allow_none": false,
            "type": "Type",
            "title": "Receivers",
            "visible": true
          }
        }
      },
      "type": {
        "visible": false,
        "default": null,
        "allow_none": false,
        "type": "StringType",
        "title": "Type",
        "readonly": true
      },
      "version": {
        "default": "0.1.0",
        "allow_none": false,
        "type": "StringType",
        "title": "Version",
        "visible": true
      }
    },
    "namespace": "nio.service.base.Service",
    "commands": {
      "status": {
        "params": {},
        "title": "status"
      },
      "runproperties": {
        "params": {},
        "title": "runproperties"
      },
      "heartbeat": {
        "params": {},
        "title": "heartbeat"
      },
      "stop": {
        "params": {},
        "title": "stop"
      },
      "start": {
        "params": {},
        "title": "start"
      }
    }
  }
}
```

  **name**<br>The name of the service type, in this case, `Service`.

  **properties**<br>The properties of the service. In this case, there is only one service type, `Service`, and all services contain these properties.

---

## Get all API

You can get the details of all the service types configurations in one request with a request to the `/services_types` endpoint.

      curl -XGET 'http://localhost:8181/services_types'
