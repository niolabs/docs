# Blocks

Blocks are the units of {{ book.product }} that send, receive, and process signals. What makes a block a block?

A block has a life cycle and at least one input terminal or one output terminal. Optionally, you can configure properties within the block. A block also has the potential to accept commands from the block REST API.

In summary, a {{ book.product }} block is:
- A unit of functionality that runs in a service
- A process that goes through the six stages of the block life cycle: configuring, configured, starting, started, stopping, stopped, (and hopefully not an error)
- A functional piece of code that receives streaming input signals and/or emits streaming output signals
- A commandable through the block REST API
- A Python class that inherits from `nio.block.base.Block`


## Properties

Properties are the configuration fields of a block.

In the System Designer, you modify the properties in the configuration panel. Properties may include rules governing how the block should process signals.

## Inputs/Outputs

A block receives or sends signals through the input and output terminals to allow interblock interaction. In the System Designer, you draw connectors between the terminals to show the signal flow.

Signals are implemented as a collection of key-value pairs. Signals are always passed between blocks inside of a list. See [Understanding Signals](/service-design-patterns/understanding-signals.md#lists-of-signals).

## Commands

Commands allow a user to interact with a running instance of a block. You can use a command to inspect the internal state of a block. When you develop a block type, you can expose certain methods in your block class as commands. This allows you to run functions inside the instance of your block from the System Designer.
