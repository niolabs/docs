# Testing \(not in MVP\)

Having confidence that changes to a block's or service's configuration do not negatively affect other services is an important part of designing robust n.io systems. Setting up "service unit tests" are one key step in gaining this confidence.

n.io provides support for defining unit tests for a service's behavior through the [Service Unit Test Framework](https://github.com/nioinnovation/service_tests). Service unit tests are written in Python code and make use of the [Python unittest module](https://docs.python.org/3/library/unittest.html).

It is recommended to put your service unit tests in a folder at the root of your project. The [n.io project template](https://github.com/nioinnovation/project_template) includes the service unit test framework under the folder `service_tests` and also contains a folder `tests` in which to put your custom service tests. This allows you to run the service tests using any Python test runner \(e.g., py.test\) from the project root, like so:

```
py.test tests
```

Note: The service unit test framework requires a n.io binary to be installed as well as the `jsonschema` Python package.

More documentation about how to use the service unit test framework can be found in the [repository's README](https://github.com/nioinnovation/service_tests).

