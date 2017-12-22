# Blocks

Blocks are nio components that perform operations on signals. Blocks can consume, alter, and/or publish signals. They are the basic unit of functionality that allows for unlimited interoperability within the nio platform.

![block illustration](/img/intro-blocks.png)

What makes a block a block?
- A block has a 6-stage life cycle: configuring, configured, starting, started, stopping, stopped. Each block in a service will match the life cycle of the service it belongs to. In other words, a block is started when its service is started.
- A block receives signals through an input terminal and/or sends signals via an output terminal to allow interblock interaction. Signals are implemented as a collection of key-value pairs and are always passed between blocks inside of a list. See [Signal Structure](/services/service-design-patterns/signal-structure.md).
- A block is a class that is written in the same language as the nio binary that it is running in. For example, in a Python nio binary, a block is a Python class that inherits from the base class nio.block.base.Block.
- Except for the most narrow-purpose blocks, a block contains configurable [properties](/blocks/properties.md).
- A block has the potential to accept commands from the block REST API.

## Commands
Commands allow a user to interact with a running configuration of a block. While the configuration API allows you view and change how a block is configured, the command API lets users work with blocks actually running inside of a service. Commands are often a useful way to perform actions on blocks without having to restart the service.

When you [develop a block type](/blocks/block-development/README.md), you can expose certain methods in your block class as commands. This allows you to run functions inside the instance of your block via the API or from the System Designer.

For example, the [Queue](https://blocks.n.io/Queue) block exposes a command to empty the internal queue. This is a better way to perform this action than restarting the entire service because the latter may negatively affect other blocks in the service.

## See Also
[Block in the System Designer](/system-designer/designer-tasks.html#blocks)

Glossary—[Block](/glossary#block)
