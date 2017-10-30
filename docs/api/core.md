# Core APIs

nio core has a few crucial API endpoints: `/nio` and `/shutdown`.  

## nio

The `/nio` endpoint is used to find information, such as versioning, about your running nio instances

    curl -XGET 'localhost:8181/nio'

The following JSON body is returned:

```json
{
    "components": {
        "ServiceMonitor": {
            "version": "0.1.0"
        },
        "ConfigManager": {
            "version": "0.1.0"
        },
        "ProjectManager": {
            "version": "2.0.0"
        },
        "LogManager": {
            "version": "0.1.0"
        },
        "BlockManager": {
            "version": "0.1.0"
        },
        "ManagementPublisher": {
            "version": "0.1.1"
        },
        "RESTManager": {
            "version": "0.1.0"
        },
        "ServiceManager": {
            "version": "0.1.0"
        }
    },
    "modules": {
        "security": {
            "BasicSecurityModule": {
                "version": "0.1.0"
            }
        },
        "settings": {
            "SettingsIniModule": {
                "version": "0.1.0"
            }
        },
        "scheduler": {
            "CustomSchedulerModule": {
                "version": "0.1.0"
            }
        },
        "communication": {
            "PubkeeperCommunicationModule": {
                "version": "0.1.0"
            }
        },
        "persistence": {
            "FilePersistenceModule": {
                "version": "0.1.0"
            }
        },
        "web": {
            "CherryPyWebModule": {
                "version": "0.1.0"
            }
        }
    },
    "nio": {
        "instance_id": "agriculture_master",
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
  - **version**<br>The version of the nio framework (not the version of the **binary**).

**start_time**<br>A datetime string that indicates when nio was started.


## Shutdown

The `/shutdown` endpoint is used to shutdown a running nio instance.

    curl -XGET 'http://localhost:8181/shutdown'

The following HTML is returned after a successful shutdown request:

    Shutdown complete
