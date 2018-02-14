# Deployment

Designing a stable nio system means having reliable mechanisms for deployment and maintenance. The deployment of nio systems is very flexible, but there are a few best practices to follow.

---
## `git` for version control

nio projects can be defined as files in a file system. Git permits you to use a standard version control system to record changes to a project. The [project template repository](https://github.com/niolabs/project_template) provides a good starting point to model how to store a project in a Git repository. With Git, you can use different branches for development and production.

---
## Different environments

You should use staging and other test environments to run nio projects outside of production. Using nio environment variable files is a good way to achieve this. For example, your project could have two configuration variable files each defining a `[user_defined]` entry `stage.conf` and `prod.conf` that define how the nio Platform should run in the respective environment. You can run nio using a different environment variable by using the `-s` flag of `niod`.

```
niod -s stage.conf
```

Sometimes, it doesn't make sense to run an individual nio service in a non-production environment. To achieve this, create an environment variable such as `SHOULD_RUN_SERVICE` and set it to `yes` or `no` depending on the environment. Then, you can set the service's auto start value in the service configuration to the result of the variable.

```
{
  "name": "ServiceName",
  "auto_start": "[[ SHOULD_RUN_SERVICE ]]"
}
```
