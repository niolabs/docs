# Services

nio services are user-configurable signal paths that run on [nio instances](/instances/README.md). They dictate how data is created, moved, transformed, and used. Services consist of multiple connected blocks. The routing of incoming/outgoing signals is defined within the nio System Designer.

![services](/img/intro-service.png)

---

A service can be as simple as the one illustrated above which takes in a data stream from a soil moisture sensor then reformats and publishes the signal for another service or UI to consume.

On the other end of the spectrum, a service can be as complicated as the one below, which subscribes to streams produced by all nio instances running within the niolabs office (door security, HVAC, laptops, etc.) and publishes that data to a UI for our team to view.

---
![agriculture system example](/img/lab-service.png)

---

The [System Designer](/system-designer/README.md) is the user interface that allows users to build services and inspect and alter the state of existing systems, instances, services, and blocks. From the System Designer, users can start/stop services, view logs, and the check the status of running services via a web browser.

Services can be started and stopped, and thus have a lifecycle of their own. Typically, each service will run in its own system process on the underlying hardware that the nio instance is running on. The nio core is responsible for spawning and monitoring these systems for you. This allows service builders to get the benefit of multiprocessing without dealing with the headaches typically associated with it.

---
## See also

* [Services in the System Designer](/system-designer/designer-tasks.md#service-sd)
* Glossary—[Service](/glossary/README.md#service)
