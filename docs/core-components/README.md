# Core Components

Part of the nio binary consists of core components. These are pieces of functionality that run alongside the nio core process. Unlike modules which run in every nio service, a core component will only be run once and will run in the core/main process.

Examples of core components include:  
  * A project manager component that exposes an API to interact with your project contents
  * A REST component that provides an interface for interacting with nio services and blocks
  * An SNMP agent component that exposes runtime information in SNMP form for easy ingestion from monitoring tools
  * A logging component that exposes an API to retrieve an instance's log messages and to change log levels for currently running services, blocks and components
  * A service monitor component that monitors service statuses able to restart a service if it becomes unresponsive

## Disabling Core Components

You cannot add core components to your binary, but you can disable existing ones if you do not want or need them. To disable a core component, in the `nio.conf` file under the `component` section, add or uncomment the disable line.

To disable the [`SNMPAgent`](/components/snmp.md) component, your `nio.conf` would look like the following example:
```
[components]
disabled=SNMPAgent
```

To disable the `Diagnostic Manager` component, your `nio.conf` would look like the following example:
```
[components]
disabled=DiagnosticManager
```

To disable the `Service Diagnostics` component, your `nio.conf` would look like the following example:
```
[diagnostic]
service=false
```

To disable the `Signals Diagnostics` component, your `nio.conf` would look like the following example:
```
[diagnostic]
signals=false
```