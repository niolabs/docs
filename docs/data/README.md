# Data Storage with nio

The nio Platform acts on streams of signals in real time and data storage is optional. But often, data storage is desired.

When designing your system, consider building services/logic close to the signal producer to pare down data storage, network transmission, and latency. [Signal flow blocks](https://blocks.n.io/?category=Signal%20Flow) like _StateChange_ and _Filter_ can be used to save (and actuate) only when specified conditions are met. A simple example service is shown below:

<img src="/img/signal-flow-service.png" style="display:block; height:300px; margin: 30px auto; border: 1px solid #ccc; border-radius: 6px;" />

To nio, a database is just another input (reading from a database is a signal producer) and/or output (writing to a database is a signal consumer). Blocks are available for most popular [datastores](https://blocks.n.io/?category=Database) ranging from CSV to open-source databases to robust enterprise solutions. If you have a data environment that does not have a block built for it yet, try using our [block development documentation](/blocks/block-development/README.md) to build your own.

An alternative to data storage is nio's persistence feature. Persistence allows services and blocks to persist data across restarts without requiring external data storage. Read more about persistence [here](/data/persistence.md).
