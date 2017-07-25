# SNMP Agent Component

The SNMP Agent core component allows you to monitor a {{ book.product }} system's health through the standard [SNMP protocol](https://en.wikipedia.org/wiki/Simple_Network_Management_Protocol).

## Behavior

The SNMP component can be configured to work as an agent that can issue traps (asynchronous) or respond to requests (synchronous) as follows:

* (asynchronous) sends traps whenever a Service changes its status, and the new status is configured as part of the `status_traps` setting.
* (synchronous) allows retrieving the system uptime and service statuses.


## Configuration

You can configure this component's behavior in your `nio.conf` file under the `[snmp]` section. The following configuration options are available:

* `host`—The host the SNMP Agent should run on (defaults to `127.0.0.1`)
* `port`—The port the SNMP Agent should run on (defaults to `161`)
* `community_index`—The name of the index to use in the SNMP community (defaults to `agent`)
* `community_name`—The name of the community (defaults to `public`)
* `trap_host`—The host the SNMP trap server should run on (defaults to `127.0.0.1`)
* `trap_port`—The port the SNMP trap server should run on (defaults to `162`)
* `trap_community_index`—The name of the index to use in the SNMP trap community (defaults to `agent`)
* `status_traps`—comma separated list of services to register status change traps for (defaults to `error`)
