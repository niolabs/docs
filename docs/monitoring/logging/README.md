# Logging

Logging is a crucial part of monitoring a running nio system. The nio Monitoring Tool allows you to view the logs of inquirable nio instances one at a time. The nio platform's logging mechanism also allows you to plug into more robust log management solutions too.

Your nio project's logging configuration uses the [Python logging](https://docs.python.org/3/library/logging.html) module and configuration. All of the logging configuration takes place in your project's `etc/logging.json` file.

## Remote Log Management

You can configure your `etc/logging.json` file to point your logs to many different types of remote logging destinations. We have guides/documentation on the following examples:

 * [AWS CloudWatch Logs](/monitoring/logging/cloud-watch.md)
