# Deployment

Designing a stable {{ book.product }} system means having reliable mechanisms for deployment and maintenance. The deployment of {{ book.product }} systems is very flexible but there are a few best practices we recommend.

## Git for Version Control

{{ book.product }} projects can be defined as files in a file system. This lends itself well to using standard version control systems such as git to maintain a record of what has changed in a project's definition. The [project template repository](https://github.com/nioinnovation/project_template) provides a good starting point for how to store a project in a git repository.

With git, you can use different branches for development and production.

## Different Environments

It is often useful to have staging or other testing environments to run {{ book.product }} projects outside of production. Using {{ book.product }} environment variable files is a good way to achieve this. For example, your project could have two environment variable files `stage.env` and `prod.env` that can each define how {{ book.product }} should run in the respective environment. You can run {{ book.product }} using a different environment variable by using the `-e` flag of `nio_run`. For example:
```
nio_run -e stage.env
```

Sometimes, it doesn't make sense to run an individual service in a non-production environment. To achieve this, create an environment variable such as `SHOULD_RUN_SERVICE` and set it to `yes` or `no` depending on the environment. Then, you can set the service's auto start value in the service configuration to the result of the variable, like so:
```
{
  "name": "ServiceName",
  "auto_start": "[[ SHOULD_RUN_SERVICE ]]"
}
```
