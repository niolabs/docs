# Component Deployment

A Component Deployment is a deferred deployment to instances that **are not** externally accessible, or a component that should self update once a new version is released. This utilizes the [nio config component](https://github.com/niolabs/component_config).

> **[info] Designer**
>
> If your instance is not externally accessible, design the configuration and [do a release](/deployment/nio/release.md) in the [nio System Designer](https://app.n.io/design) using a [cloud instance](/quickstart/README.md) or an accessible local instance.
>

## Doing a Component Deployment

> **[danger] Requirements**
>
> An initial [release](/deployment/nio/release.md) must be done before a deployment can be done.
>

#### To do a component deployment:
- Make sure your nio instance has the [nio deployment API component](https://github.com/niolabs/component_deployment_api).
- Get the Instance Configuration ID from the Release modal in the System Designer.

<img class="left border" src="/img/deploy/component/id.png" height="350" />

- Copy the **id** value for the configuration you would like to use.
- Paste that value into your `nio.conf` file under the `[configuration]` section.
- Update the **config_poll_interval** value to the number of seconds you would like the component to check if an update is available. In this example we will use 60 minutes.
- Your `nio.conf` `[configuration]` section should look like this:

```
[configuration]
config_id=id-copied-from-designer
config_poll_interval=3600
# specifies if modified services are to be started/stopped based on the
# auto_start flag
#start_stop_services=True

# specifies if existing blocks and services are to be deleted when not found
# in the incoming configuration
#delete_missing=True
```

- That's all the configuration necessary for the config component. You can now run nio and do a [new release](/deployment/nio/release.md) and your nio instance will sync itself to the updated version!
