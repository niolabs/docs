# nio Deploy

The nio deployment application, found at [app.n.io/deploy](https://app.n.io/deploy), is the graphical user interface used to deploy a version of an instance out to other instances.

## Terms
#### Instance Configuration

An Instance Configuration is similar to a **repository** on github. The idea is the Instance Configuration is *designed* in the [System Designer](https://app.n.io/design) only once, but can then can be deployed out to many instances which all need to run the exact same Configuration.

#### Instance Configuration Version

An Instance Configuration Version is similar to a **release** on github. An Instance Configuration Version must belong to an Instance Configuration, can be named using any versioning scheme, we recommend [semver](https://semver.org), and must be unique.

An Instance Configuration Version is a point in time snapshot of an Instance Configuration. This can be useful, for example, if an update is deployed to a production system which does not function as intended and needs to be rolled back to a previous working version.

---

## Release

In order to do an initial deployment, first a new instance configuration must be released.

* [Release Cycle](/deployment/nio/release.md) 

---

## Deploy

After successfully releasing an instance configuration

* [Direct Deployment](/deployment/nio/direct.md)
* [Component Deployment](/deployment/nio/component.md)
