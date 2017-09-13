# Service Unit Testing

Testing is a necessary part of designing a robust system. To ensure your block or service configurations are performing correctly, you need to set up service unit tests.

Use the the [Service Unit Test Framework](https://github.com/niolabs/service_tests) to define unit tests for a service's behavior. Service unit tests are written in Python code and make use of the [Python unittest module](https://docs.python.org/3/library/unittest.html).

If you installed the [project template](https://github.com/niolabs/project_template) from the repository, then you are ready. If not, complete the following steps:

1. Install the `jsonschema` Python package. This allows you to validate publishers and subscribers in services.
2. Clone the [{{ book.product }} Service Units Test](https://github.com/niolabs/service_tests) repository into your project directory as a submodule.
3. Create a `tests` directory to store your own custom service unit tests.
4. Set up a test class based on the [Service Unit Test](https://github.com/niolabs/service_tests) readme file.
4. Execute the service tests using a Python test runner.
```
py.test tests
```
