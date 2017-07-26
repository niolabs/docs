# SNMP Agent Component

The SNMP Agent core component allows you to monitor the health of a {{ book.product }} system through the standard [SNMP protocol](https://en.wikipedia.org/wiki/Simple_Network_Management_Protocol).

## Behavior

The SNMP component can be configured to work as an agent that can issue traps asynchronously or respond to requests synchronously.

* Asynchronous mode sends traps whenever a service changes its status, and the new status is configured as part of the `status_traps` setting.
* Synchronous mode allows retrieving the system uptime and service statuses.


## Configuration

You can configure the behavior of this component in your `nio.conf` file under the `[snmp]` section. 

The following configuration options are available:

* `host`—The host address for the SNMP Agent (default=`127.0.0.1`)
* `port`—The port for the SNMP Agent (default=`161`)
* `community_index`—The name of the index to use in the SNMP community (default=`agent`)
* `community_name`—The name of the community (default=`public`)
* `trap_host`—The host address for the SNMP trap server (default=`127.0.0.1`)
* `trap_port`—The port for the SNMP trap server (default=`162`)
* `trap_community_index`—The name of the index to use in the SNMP trap community (default=`agent`)
* `status_traps`—The comma separated list of services to register status change of traps (default=`error`)
