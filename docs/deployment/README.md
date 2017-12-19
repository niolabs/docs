# Deployment

Designing a stable nio system means having reliable mechanisms for deployment and maintenance. The deployment of nio systems is very flexible, but there are a few best practices to follow.

## Git for Version Control

nio projects can be defined as files in a file system. Git permits you to use a standard version control system to record changes to a project. The [project template repository](https://github.com/niolabs/project_template) provides a good starting point to model how to store a project in a Git repository. With Git, you can use different branches for development and production.

## Different Environments

You should use staging and other test environments to run nio projects outside of production. Using nio environment variable files is a good way to achieve this. For example, your project could have two environment variable files `stage.env` and `prod.env` that define how nio should run in the respective environment. You can run nio using a different environment variable by using the `-e` flag of `nio_run`.
```
nio_run -e stage.env
```

Sometimes, it doesn't make sense to run an individual service in a non-production environment. To achieve this, create an environment variable such as `SHOULD_RUN_SERVICE` and set it to `yes` or `no` depending on the environment. Then, you can set the service's auto start value in the service configuration to the result of the variable.
```
{
  "name": "ServiceName",
  "auto_start": "[[ SHOULD_RUN_SERVICE ]]"
}
```
