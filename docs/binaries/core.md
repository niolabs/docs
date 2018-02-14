# nio core

The nio core is the engine that runs in every nio binary. It is responsible for orchestrating all the different pieces that constitute the nio instance. In most cases, the core will run in its own main process and will spawn services in their own individual operating system processes. This allows those who are creating services to make use of multiprocessing by splitting their logic across different services. The core process will take care of setting up the appropriate IPC pipes and will monitor the lifecycle of the service process.

---

## Block and service managers

The core contains manager components that are responsible for keeping track of the types of blocks and configurations of services. We call these components that keep track of their corresponding resources the **Block Manager** and the **Service Manager**, respectively.

[Block](/blocks) types correspond to the different blocks that are installed in the instance. While having multiple service types is possible, almost all nio instances currently ship with only one type of service that we cleverly call `Service`. This service type is the type used for every service in an instance. In the future, additional service types may be included to perform different types of functions.

The **Service Manager** is responsible for launching service processes and maintaining a persistent connection to them via an IPC pipe. Commands to the service such as fetching its status or commanding a block can be passed from the core to the service process through its pipe.

---

## Auto discovery

One of the core's main functions is managing the different modules, components, blocks, and services that exist within a nio instance. It includes an auto-discovery mechanism to find each of these. Based on the configuration in your project's `nio.conf` file, the core will walk through the Python namespace searching for objects that match the signature of the resources. For example, the core's discoverability mechanism will walk the namespace of `niocore.components` searching for discoverable classes that are subclasses of the `Component` class.

You can control the discoverability of classes using the `@discoverable` and `@not_discoverable` [decorators](https://github.com/niolabs/nio/blob/master/nio/util/discovery.py) included in the nio development framework. Marking a class as discoverable or not discoverable will not transfer to its subclasses. You must explicitly define the discoverability of each subclass. Note that classes of type `Block` and `Service` are automatically discoverable, but classes of type `Component` are not automatically discoverable.
