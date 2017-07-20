# Service Unit Testing

Testing is a necessary part of designing a robust system. To ensure your block or service configurations are performing correctly, you need to set up service unit tests.

In order to have confidence that changes to a block or service configuration do not negatively affect other services, testing is necessary and it an important part of designing robust {{ book.product }} systems. To gain this confidence, set up service unit tests. 
Use the the [Service Unit Test Framework](https://github.com/nioinnovation/service_tests) to define unit tests for a service's behavior. Service unit tests are written in Python code and make use of the [Python unittest module](https://docs.python.org/3/library/unittest.html).

1. If you are validating publisher or subscriber services, install the `jsonschema` Python package.
2. Clone the [n.io Service Units Test](https://github.com/nioinnovation/service_tests) repo into your project directory.
3. Create a `tests` directory.
4. Set up a test class. See [Service Unit Test repository's README](https://github.com/nioinnovation/service_tests). 
4. Execute the service tests using a Python test runner.
```
py.test tests
```



=====OLD TEXT BELOW


In order to have confidence that changes to a block or service configuration do not negatively affect other services, testing is necessary and it an important part of designing robust {{ book.product }} systems. To gain this confidence, set up service unit tests. 

More documentation about how to use the service unit test framework can be found in the [Service Unit Test repository's README](https://github.com/nioinnovation/service_tests).




Service unit tests can be put in a folder at the root of your project. The [n.io project template](https://github.com/nioinnovation/project_template) includes the service unit test framework under the folder `service_tests` and also contains a folder `tests` where you can put your custom service tests. This allows you to run the service tests using any Python test runner \(e.g., py.test\) from the project root, like so:

```
py.test tests
```

Note: The service unit test framework requires a {{ book.product }} binary to be installed as well as the `jsonschema` Python package.

More documentation about how to use the service unit test framework can be found in the [Service Unit Test repository's README](https://github.com/nioinnovation/service_tests).
