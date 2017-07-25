# Core Components

Part of the {{ book.product }} binary consists of core components. These are pieces of functionality that run alongside the {{ book.product }} core process. Unlike modules which run in every {{ book.product }} service, a core component will only be run once and will run in the core/main process.

Communications protocols such as ZMQ, HTTP, and SNMP are examples of {{ book.product }} core components. 

## Disabling Core Components

Your binary will include some core components. You cannot add core components to your binary but you can disable existing ones if you do not want or need them. To do so, in your `nio.conf` file add (or uncomment) the disable line under the `component` section. For example, to disable the [`SNMPAgent`](/components/snmp.md) component, your `nio.conf` should look like the following:
```
[components]
disable=SNMPAgent
```
