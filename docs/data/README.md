# Data Storage with nio

nio acts on streams of signals in real-time. Data storage is not required in nio–although it may be useful.

When designing your system, consider building services/logic close to the signal producer to pare down data storage, network transmission, and latency. [Signal flow blocks](https://blocks.n.io/?category=Signal%20Flow) like _StateChange_ and _Filter_ can be used to save (and actuate) only when specified characteristics are met. A simple example service is shown below:

![signal flow service](/img/signal-flow-service.png)

To nio, a database is just another input (read = signal producer) and/or output (write = signal consumer). Blocks are available for most popular datastores ranging from CSV to open-source databases to robust enterprise solutions. If you have a data environment that does not have a block built for it yet, try using our [block development documentation](/blocks/block-development/README.md) to build your own.

Persistence is also a helpful nio signal management feature that allows services and blocks to persist data across restarts. Read more about persistence [here](/data/persistence.md).
