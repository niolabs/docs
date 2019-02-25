# Logging using AWS CloudWatch Logs

If you have an AWS environment it can be helpful to integrate your nio instance's logs with AWS CloudWatch Logging. This allows you to view your nio instances' logs in the AWS console.

## Requirements

 * [watchtower](https://github.com/kislyuk/watchtower) - We will make use of the popular watchtower Python library to ship our logs to AWS CloudWatch
 * AWS Credentials - You will also need to load AWS credentials on the device running nio.

## Setup

First, install watchtower. Be sure to add this dependency to your project's `requirements.txt` or build pipeline if you have one.

```
pip install watchtower
```

Then, you can either set the default AWS environment variables on your device or create a [boto profile](http://boto.cloudhackers.com/en/latest/boto_config_tut.html#credentials) containing the necessary credentials. The example here will assume setting the default AWS environment variables.

Note: these environment variables must be set in the environment that nio is running in. For example, if you run nio using systemd then you will need to set the variables there using the [systemd environment directive](https://coreos.com/os/docs/latest/using-environment-variables-in-systemd-units.html).

```bash
export AWS_ACCESS_KEY_ID = 'your access key'
export AWS_SECRET_ACCESS_KEY = 'your secret access key'
export AWS_REGION_NAME = 'your region'
```

## Logging Config

Next, update your logging config (`etc/logging.json`) to push logs to AWS. The only requirement is a new handler. Add an entry to the "handlers" item in the config that looks like this:

```json
"handlers": {
	"watchtower": {
	  "level": "INFO",
	  "formatter": "default",
	  "filters": ["niofilter"],
	  "()": "watchtower.CloudWatchLogHandler",
	  "log_group": "[[INSTANCE_ID]]",
	  "stream_name":  "nio",
	  "send_interval": 1,
	  "create_log_group": true
	}
}
```

You will also want to bind the root logger to your new handler by adding the `watchtower` handler to the list of handlers for the `root` item.

This will publish logs to a CloudWatch log group with your instance ID as the name. The log stream will be called "nio". Description of these parameters and additional configuration parameters can be found in the [watchtower documentation](https://github.com/kislyuk/watchtower).

There is some redundant information in these logs though that we don't really need. For example, the timestamp and the string NIO appear but we already have that information from AWS. To clean these up, we can create a new formatter called "aws" that doesn't have this unnecessary information.

```json
"formatters": { 
	"aws": {
		"format": "[%(levelname)s] [%(context)s] %(message)s"
	}
}
```

Then, replace the old "default" formatter in the handler config with "aws" to use our new formatter.

## Full Config

When you're all said and done, your `etc/logging.json` may look something like this:
```json
{
    "version": 1,
    "disable_existing_loggers": false,
    "formatters": {
        "default": {
            "format": "[%(niotime)s] NIO [%(levelname)s] [%(context)s] %(message)s"
        },
        "aws": {
            "format": "[%(levelname)s] [%(context)s] %(message)s"
        }
    },
    "filters": {
        "niofilter": {
            "()": "nio.util.logging.filter.NIOFilter"
        },
        "log_signal_filter": {
            "()": "nio.util.logging.handlers.publisher.log_signal_filter.LogSignalFilter"
        },
        "cache_filter": {
            "()": "nio.util.logging.handlers.publisher.cache_filter.CacheFilter",
            "expire_interval": 0.2
        }
    },
    "handlers": {
        "default": {
            "level": "DEBUG",
            "class": "logging.StreamHandler",
            "stream": "ext://sys.stdout",
            "formatter": "default",
            "filters": ["niofilter"]
        },
        "file": {
            "level": "DEBUG",
            "class": "nio.util.logging.handlers.file_handler.NIOFileHandler",
            "filename": "__service_name__",
            "dirname": "[[PROJECT_ROOT]]/logs",
            "formatter": "default",
            "filters": ["niofilter"]
        },
        "comm": {
            "level": "INFO",
            "class": "nio.util.logging.handlers.publisher.handler.PublisherHandler",
            "topic": "nio_logging.[[INSTANCE_ID]].__service_name__",
            "formatter": "default",
            "filters": ["niofilter", "log_signal_filter", "cache_filter"]
        },
        "watchtower": {
          "level": "INFO",
          "formatter": "aws",
          "filters": ["niofilter"],
          "()": "watchtower.CloudWatchLogHandler",
          "log_group": "[[INSTANCE_ID]]",
          "stream_name":  "nio",
          "send_interval": 1,
          "create_log_group": true
        }
    },
    "root": {
        "handlers": ["default", "file", "comm", "watchtower"],
        "level": "WARNING"
    },
    "loggers": {
        "main": {
            "level": "NOTSET"
        },
        "main.WebServer": {
            "level": "INFO"
        },
        "main.ServiceManager": {
            "level": "INFO"
        },
        "pubkeeper": {
            "level": "INFO"
        }
    }
}
```

