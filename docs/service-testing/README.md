# Service Testing

In order to have confidence that changes to a block or service configuration do not negatively affect other services, testing is necessary and it an important part of designing robust {{ book.product }} systems. To gain this confidence, set up service unit tests. 

Use the the [Service Unit Test Framework](https://github.com/nioinnovation/service_tests) to define unit tests for a service's behavior. Service unit tests are written in Python code and make use of the [Python unittest module](https://docs.python.org/3/library/unittest.html).


1. Install the {{ book.product }} binary and the `jsonschema` Python package.
2. Copy the service unit test framework from the `service_tests` folder in the [n.io project template](https://github.com/nioinnovation/project_template)  to a folder in the root of your project.
3. Copy the `tests` folder to a folder in the root of your project.
4. Execute the service tests using a Python test runner.
```
py.test tests
```

See the [Service Unit Test repository's README](https://github.com/nioinnovation/service_tests) to learn more about the service unit test framework.


=====OLD TEXT BELOW

More documentation about how to use the service unit test framework can be found in the [Service Unit Test repository's README](https://github.com/nioinnovation/service_tests).




Service unit tests can be put in a folder at the root of your project. The [n.io project template](https://github.com/nioinnovation/project_template) includes the service unit test framework under the folder `service_tests` and also contains a folder `tests` where you can put your custom service tests. This allows you to run the service tests using any Python test runner \(e.g., py.test\) from the project root, like so:

```
py.test tests
```

Note: The service unit test framework requires a {{ book.product }} binary to be installed as well as the `jsonschema` Python package.

More documentation about how to use the service unit test framework can be found in the [Service Unit Test repository's README](https://github.com/nioinnovation/service_tests).
