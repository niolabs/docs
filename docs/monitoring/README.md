# Monitoring

After deploying a software solution, the task becomes monitoring it. With the nio Platform, it is easy to monitor the environment of nio instances. But in many cases, this is not granular enough for your needs because there is no visibility of the environment at the nio-service level.

---

## Third-party tools

If you are already using a third-party monitoring solution and wish to monitor your nio deployment using that same tool, you have the ability to have nio report metrics to be visualized in your existing dashboards.

nio has blocks that integrate with [Google Stackdriver](https://cloud.google.com/stackdriver/) and [Datadog](https://www.datadoghq.com/). To access guides on how to monitor nio with these third-party tools, visit the following sections:

* [Google Stackdriver](/monitoring/stackdriver.md)
* [Datadog](/monitoring/datadog.md)
