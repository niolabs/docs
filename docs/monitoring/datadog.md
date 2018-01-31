# Datadog

To integrate the nio Platform into your [Datadog](https://app.datadoghq.com/) account, use the _DatadogCustomMetrics_ nio block to begin monitoring individual nio services.

---

## How to use

The [_DatadogCustomMetrics_](https://blocks.n.io/DatadogCustomMetrics) nio block can be added to your nio services to post custom metrics to your Datadog dashboard. You can configure your nio service to post any custom metric values that you wish to monitor.

### Monitoring a service

The [_ProcessMetrics_](https://blocks.n.io/ProcessMetrics) and _DatadogCustomMetrics_ blocks can be used together to monitor the environment that the service is running in.

>**[info] Service process ID**
>
>Setting the **PID** property to {% raw %}`{{ __import__('os').getpid() }}`{% endraw %} in the _ProcessMetrics_ block will obtain the process ID of the service containing the block.

#### Displaying the data in Datadog

On the Datadog dashboard where you want to view your nio metrics, create a new **timeseries** graph. Click the JSON tab in the graph editor window. In the **requests** section of the JSON, change the **q** value from the default value to the value you configured in the _DatadogCustomMetrics_ block (i.e., `nio.<service name>`).

Your JSON configuration should look similar to what follows:

```JSON
{
  "viz": "timeseries",
  "status": "done",
  "requests": [
    {
      "q": "nio.<service name>{*}",
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

Save the graph configuration, start the service, and you will start seeing data points appear on the timeseries graph.
