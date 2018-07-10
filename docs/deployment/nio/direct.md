# Direct Deployment

A Direct Deployment is an instant deployment to instances that **are** externally accessible. 

> **[info] Compatibility**
>
> If you can load your instance in the System Designer, you can do a Direct Deployment to it.
>

## Doing a Direct Deployment

> **[danger] Requirements**
>
> A [Release](/deployment/nio/release.md) must be done before a deployment can be done.
>

- To do a direct deployment, navigate to the deployment tool on [app.n.io/deploy](https://app.n.io/deploy).
- Next click the **Deploy** button in the top right corner.

<img class="left" src="/img/deploy/direct/button.png" />

---

- Select the System with which you would like to deploy to.
- You will then be prompted with the new Deployment Page:

<img src="/img/deploy/direct/new.png" />

---

- Notice the instances on bottom. They need to be assigned to the configuration that should be deployed.

<img src="/img/deploy/direct/assign.png" />

---

- Assign all the instances that need to be deployed to.

<img src="/img/deploy/direct/assigned.png" />

---

- The next step is to select the correct version to deploy for each configuration.

<img src="/img/deploy/direct/version.png" />

---

- After that is done, review the deployment and if everything looks correct click `deploy`!
- The deployment will begin and will report it's progress when complete. 

<img src="/img/deploy/direct/complete.png" />

---

## Deployment Details

- The deployment can be clicked on to view specific details about each instance that was deployed to. For instance, if the deployment is reporting as failed, you can click in and investigate which instance in particular may have caused the failure.

<img src="/img/deploy/direct/details.png" />