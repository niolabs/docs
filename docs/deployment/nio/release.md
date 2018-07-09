# Release Cycle

Releasing a new or updated nio instance is similar to releasing a new version on github.

## Doing a Release

To do the first release, first click the Release button in the Instance toolbar:

<img class="left" src="/img/deploy/release/toolbar.png" />

### Creating a new Instance Configuration

This will show the option to create a a new Instance Configuration. Give your Instance Configuration a name and an initial version. We recommend `v1.0.0` which follows the [semver](https://semver.org) scheme.

<img class="left" src="/img/deploy/release/modal.png" height="350" />

Click `OK` to release your first Instance Configuration!

If you would now like to deploy, you should move on to:

* [Direct Deployment](/deployment/nio/direct.md)
* [Release Deployment](/deployment/nio/release.md)

### Releasing a new Version

If an Instance Configuration is already created and only a new version needs to be released, select the Instance Configuration from the select field and then give the version a new number. Remember, an Instance Configuration Version can be named using any versioning scheme, we recommend [semver](https://semver.org), and must be unique.

<img class="left" src="/img/deploy/release/version.png" height="350" />

Click `OK` to release the new Instance Configuration Version!

---

## Deploy

After successfully releasing an instance configuration

* [Direct Deployment](/deployment/nio/direct.md)
* [Component Deployment](/deployment/nio/component.md)