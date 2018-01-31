# Google Stackdriver

To integrate the nio Platform into your [Google Stackdriver](https://cloud.google.com/stackdriver/) account, use the _StackdriverCustomMetrics_ nio block to begin monitoring individual nio services.

---

## How to use

The [_StackdriverCustomMetrics_](https://blocks.n.io/StackdriverCustomMetrics) nio block can be added to your nio services to post custom metrics to your Google Stackdriver dashboard. You can configure your nio service to post any custom metric values that you wish to monitor.

### Monitoring a service

The [_ProcessMetrics_](https://blocks.n.io/ProcessMetrics) and _StackdriverCustomMetrics_ blocks can be used together to monitor the environment that the service is running in.

>**[info] Service process ID**
>
>Setting the **PID** property to {% raw %}`{{ __import__('os').getpid() }}`{% endraw %} in the _ProcessMetrics_ block will obtain the process ID of the service containing the block.

#### Finding the data in Stackdriver

The custom metric reported via nio can be found in the Stackdriver Metrics Explorer.
