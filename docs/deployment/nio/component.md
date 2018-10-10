# Indirect Deployment

An Indirect Deployment is a deferred deployment to instances that **are not** directly accessible from the nio Management App. Rather than directly informing an instance of the configuration that it should be running like a [direct deployment](/deployment/nio/direct.md), the instance will instead periodically poll the nio API for instance configuration information.

This type of deployment is convenient when instances aren't always running or when they are running behind a firewall and can't be directly accessed.

> **[info] nio Version**
>
> For the best deployment experience, we recommend running at least the **20181009** version of the nio binary. It may be possible to perform an indirect deployment with an older binary, contact nio support for help with that.
>

## Perform an Indirect Deployment

To perform an Indirect Deployment make sure your instance is set up for indirect deployments by following the instructions below. If it is, when you add your instance to the deployment just select "Indirect" for the deployment mode of the instance from the nio Deployment Manager. Once the deployment is started, the nio instance will receive the new configuration the next time it checks in. You can check on the status of the deployment from the deployment status page. The following statuses describe the lifecycle of an indirect deployment:

 - *Started* - The deployment has been created but the instance has not checked in yet
 - *Accepted* - The nio instance has checked in and pulled down the latest configuration data
 - *Success* - The nio instance has successfully applied and is running the configuration data
 - *Error* - The nio instance encountered a problem applying the configuration. See the error message and/or check your instance logs for specific reasons as to why this didn't work.

## Setting up Your Instance

Setting up your nio instance for performing an indirect deployment means telling your instance to periodically check with the nio API for configuration information. To do this, add the following configuration to your instance's configuration (`nio.conf`):

```
[configuration]
config_poll_interval = 3600
```

The **config_poll_interval** setting is the number of seconds between instance polls. For example, **3600** means the instance will check for a new configuration every hour.


### Advanced Options

The nio deployment component takes some additional advanced configuration options, all contained under the `[configuration]` section of settings.

 - **start_stop_services** - defaults to *true* - Whether or not to start auto-start services and stop non-auto-start services.
 - **delete_missing** - defaults to *true* - Whether or not to delete services and blocks that are missing from the configuration. The default of true means that configuration payloads will contain the entire instance configuration. Set this to *false* in order to perform "partial" deployments.
 - **config_api_url_prefix** - The API URL to hit when fetching configuration information. Only change this if you have another API set up to deliver configuration payloads
 - **config_id** - Use this setting to explicitly set the configuraiton ID that the instance is running
 - **config_version_id** - Use this setting to explicitly set the configuration version ID that the instance is running

### Deployment Logging

By default non-error conditions in the deployment component will not be logged to your instance logs. In order to enable some more verbose logging for troubleshooting purposes you can configure the **main.DeploymentManager** logger in your `etc/logging.json` file.

Example:
```
{
    ...
    "loggers": {
	    "main.DeploymentManager": {
		    "level": "DEBUG"
		}
	}
}
```

### Instance ID and API Key

In order to conduct a deployment the nio instance must know its instance ID and have a valid API key assigned to it. Connecting to the instance via the nio System Designer should set these values on the instance for you. You can explicitly set the instance's ID and API key by setting the `INSTANCE_ID` and `API_KEY` variables respectively through environment variables or your `nio.conf` file.

Check to make sure your instance ID and API key are correct by hitting the `/instance/api_key` endpoint on your nio instance. For example:
```
$ curl -u Admin:Admin https://localhost:8181/instance/api_key
{"api_key": "00000000-0000-0000-0000-000000000000", "instance_id": "00000000-0000-0000-0000-000000000000"}
```


