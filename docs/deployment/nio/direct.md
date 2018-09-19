# Direct Deployment

A Direct Deployment is an instant deployment to instances that **are** externally accessible.

> **[info] Compatibility**
>
> If you can load your instance in the System Designer, you can deploy directly to it.
>

## Configuration

A few options can be set under the `configuration` section of your `nio.conf` file:
```
[configuration]
# specifies if modified services are to be started/stopped based on the
# auto_start flag
#start_stop_services=True

# specifies if existing blocks and services are to be deleted when not found
# in the incoming configuration
#delete_missing=False
```

## Doing a Direct Deployment

> **[danger] Requirements**
>
> A [release](/deployment/nio/release.md) must be done before a deployment can be done.
>

- To do a direct deployment, navigate to the deployment tool on [app.n.io/deploy](https://app.n.io/deploy).
- Next click the **deploy** button in the top right corner.

<img class="left" src="/img/deploy/direct/button.png" />

---

- Select the system with which you would like to deploy to.
- You will then be prompted with the new Deployment Page:

<img src="/img/deploy/direct/new.png" />

---

- Notice the instances at the bottom. They need to be assigned to the configuration that should be deployed.

<img class="border" src="/img/deploy/direct/assign.png" />

---

- Assign all the instances that need to be deployed to.

<img src="/img/deploy/direct/assigned.png" />

---

- The next step is to select the correct version to deploy for each configuration.

<img src="/img/deploy/direct/version.png" />

---

- After that is done, review the deployment and if everything looks correct click **deploy**!
- The deployment will begin and will report its progress when complete.

<img src="/img/deploy/direct/complete.png" />

---

## Deployment Details

- The deployment can be clicked on to view specific details about each instance that was deployed to. For instance, if the deployment reported as failed, you can click in and investigate which instance in particular may have caused the failure.

<img src="/img/deploy/direct/details.png" />
