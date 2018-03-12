# Instances

nio instances are running versions of the nio Platform. They, along with [user interfaces](/ui/README.md) and [Pubkeeper](/pubkeeper/README.md), are the entities that work cooperatively together to form a nio [system](/systems/README.md).

nio can be installed on a chip, cloud, and anything in between, so instances come in all shapes and sizes. Having multiple distinct instances in a system enables distributed processing and intelligence.

All instances run on some form of compute. We have specialized nio [binaries](/binaries/README.md) to accommodate various instance locations, environments, and functionality.

A single instance of nio can have multiple [services](/services/README.md) with related or unrelated functions. In general, each device or cloud instance will run one instance of nio. However, running parallel instances of nio is possible and is sometimes helpful for failover and load balancing.

![instances](/img/intro-instance.png)

**Instance with multiple interrelated services used for precision agriculture.**

Where you decide to install nio instances (or logic) throughout a system should ultimately be determined by the desired outcome and constraints of your specific application. These decisions are usually made during the design and solution architecture phase of a project.

---
## See also

* [Instances in the System Designer](/system-designer/designer-tasks.md#instance-sd)
* Glossary—[instance](/glossary/README.md#instance)
