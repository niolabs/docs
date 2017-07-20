# Service Unit Testing

Testing is a necessary part of designing a robust system. To ensure your block or service configurations are performing correctly, you need to set up service unit tests.
 
Use the the [Service Unit Test Framework](https://github.com/nioinnovation/service_tests) to define unit tests for a service's behavior. Service unit tests are written in Python code and make use of the [Python unittest module](https://docs.python.org/3/library/unittest.html).

1. Install the `jsonschema` Python package. This allows you to validate publishers and subscribers in services.
2. Clone the [n.io Service Units Test](https://github.com/nioinnovation/service_tests) repo into your project directory as a submodule.
3. Create a `tests` directory to store your own custom service unit tests.
4. Set up a test class. See the [Service Unit Test](https://github.com/nioinnovation/service_tests) repository's readme file. 
4. Execute the service tests using a Python test runner.
```
py.test tests
```
