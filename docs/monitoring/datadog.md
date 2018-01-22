# Datadog

To integrate the nio Platform into your [Datadog](https://app.datadoghq.com/) account to begin monitoring individual nio services, you will need to add three simple blocks into the service(s) you wish to monitor. This section outlines how to configure and connect those block to send data up to Datadog and how to configure your graph in Datadog to display that data.

---

## How to use

The [_DatadogCustomMetrics_](https://blocks.n.io/DatadogCustomMetrics) nio block can be added to your nio services to post custom metrics to your Datadog dashboard. You can configure your nio service to post any custom metric values that you wish to monitor.

### Monitoring a service

The following example explains how to configure your service to send metrics about itself up to your Datadog dashboard. Three additional blocks will need to be added to your service in order to integrate with Datadog:

* [_IdentityIntervalSimulator_](https://blocks.n.io/IdentityIntervalSimulator)
* [_ProcessMetrics_](https://blocks.n.io/ProcessMetrics)
* [_DatadogCustomMetrics_](https://blocks.n.io/DatadogCustomMetrics)

#### Configure the blocks

The _IdentityIntervalSimulator_ block will trigger nio to send data up to Datadog. Configure the block to send a signal every minute.

The _ProcessMetrics_ block should be configured to send the data that you are most interested monitoring. In the block configuration, select the checkboxes next to the metrics that you will monitor. In the **PID** property, set the value to `{{ __import__('os').getpid() }}`. This gets the process ID of the running service so that it can report data on itself. You will know if the service has gone into an error state if metrics have stopped reporting to your dashboard.

<img class="right display" src="/img/monitoring/datadog-monitoring-service.png" height="325" />

The _DatadogCustomMetrics_ block needs the following properties configured to report your data:

* **API Key**: your Datadog application API key. This can be found in the Integrations > API section of your account.
* **App Key**: your Datadog application key. This value can be generated on the same page as the API key.
* **Metric**: the name of the metric you are monitoring. This value needs to match the value you configure in your Datadog graph. (i.e., `nio.<service name>`)
* **Value**: the value to be graphed in Datadog's dashboard. This will likely be a value output by the _ProcessMetrics_ block. (i.e., {% raw %}`{{ $memory_percent }}`{% endraw %} or {% raw %}`{{ $cpu_percentage }}`{% endraw %})

Connect the output terminal of the _IdentityIntervalSimulator_ block to the input terminal of the _ProcessMetrics_ block and connect the output terminal of the _ProcessMetrics_ block to the input terminal of the _DatadogCustomMetrics_ block.

#### Displaying the data in Datadog

On the Datadog dashboard that you want to add your nio metrics to, create a new **timeseries** graph. Click the JSON tab in the graph editor window. In the **requests** section of the JSON, change the **q** value from the default value to the value you configured in the _DatadogCustomMetrics_ block (i.e., `nio.<service name>` if you followed along with this example).

Your JSON configuration should look similar to what follows:

```JSON
{
  "viz": "timeseries",
  "status": "done",
  "requests": [
    {
      "q": "nio.service{*}",
      "type": "line",
      "style": {
        "palette": "dog_classic",
        "type": "solid",
        "width": "normal"
      },
      "conditional_formats": [],
      "aggregator": "avg"
    }
  ],
  "autoscale": true
}
```

Save the graph configuration, start the service, and you will start seeing data points appear on the timeseries graph. You are now successfully monitoring a nio service!
