# Components

Components are optional pieces of functionality that can be included in a nio [binary](/binaries/README.md) and r un in the core process. They provide a means to augment the features that are included in a nio binary.

For example, a core component may be responsible for managing an instance’s blocks. This component could expose an API that allows users to fetch and/or upgrade their blocks. This makes sense to run as a component rather than a [module](/binaries/modules.md) because it only needs to run once per instance and it doesn’t expose functionality that blocks need to use.

Currently, development of core components requires core source-code access. Eventually the component base classes may be moved to the development framework.

## Disabling Core Components
You cannot add core components to your binary, but you can disable existing ones if you do not want or need them. To disable a core component, in the `nio.conf` file under the component section, add or uncomment the disable line.
To disable the SNMPAgent component, your `nio.conf` would look like the following example:
```
[components]
disabled=SNMPAgent
```


To disable the Diagnostic Manager component, your `nio.conf` would look like the following example:
```
[components]
disabled=DiagnosticManager
```


To disable the Service Diagnostics component, your `nio.conf` would look like the following example:
```
[diagnostic]
service=false
```


To disable the Signals Diagnostics component, your `nio.conf` would look like the following example:
```
[diagnostic]
signals=false
```
