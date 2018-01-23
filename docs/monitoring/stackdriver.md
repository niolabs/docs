# Google Stackdriver

To integrate the nio Platform into your [Google Stackdriver](https://cloud.google.com/stackdriver/) account to begin monitoring individual nio services, you will need to add three simple blocks into the service(s) you wish to monitor. This section outlines how to configure and connect those block to post data to Stackdriver and how to configure your graph in Stackdriver to display that same data.

---

## How to use

The [_StackdriverCustomMetrics_](https://blocks.n.io/StackdriverCustomMetrics) nio block can be added to your nio services to post custom metrics to your Google Stackdriver dashboard. You can configure your nio service to post any custom metric values that you wish to monitor.

### Monitoring a service

The following example explains how to configure your service to send metrics about itself up to your Google Stackdriver dashboard. Three additional blocks will need to be added to your service in order to integrate with Stackdriver:

* [_IdentityIntervalSimulator_](https://blocks.n.io/IdentityIntervalSimulator)
* [_ProcessMetrics_](https://blocks.n.io/ProcessMetrics)
* [_StackdriverCustomMetrics_](https://blocks.n.io/StackdriverCustomMetrics)

#### Configure the blocks

The _IdentityIntervalSimulator_ block will trigger nio to post data to Stackdriver. Configure the block to send a signal every minute.

The _ProcessMetrics_ block should be configured to send the data that you are most interested monitoring. In the block configuration, select the checkboxes next to the metrics that you will monitor. In the **PID** property, set the value to `{{ __import__('os').getpid() }}`. This gets the process ID of the running service so that it can report data on itself. You will know if the service has gone into an error state if metrics have stopped reporting to your dashboard.

<img class="right display" src="/img/monitoring/stackdriver-monitoring-service.png" height="325" />

The _StackdriverCustomMetrics_ block needs the following properties configured to report your data:

#### Displaying the data in Stackdriver

In you Stackdriver account, 
