# Blocks

Blocks are the units of {{ book.product }} that do the work to send, receive, and process signals. What makes a block a block?

A block has a **lifecycle** and at least one **input** terminal or one **output** terminal. Inside the block are optional **properties** which allow the block to be configured. Finally, a block has the potential to accept **commands** from the block REST API.

In sum, a {{ book.product }} block is:
- a unit of functionality that runs in a service
- "runnable"—meaning it goes through the six stages of the block life cycle: configuring, configured, starting, started, stopping, stopped, (error)
- a functional piece of code that receives streaming input signals and/or emits streaming output signals
- commandable through the block REST API
- a Python class that inherits from `nio.block.base.Block`


## Properties

Properties are the configuration fields of a block.

In the System Designer, the block's properties are the fields that appear in the configuration panel. Properties can include rules about how the block should process signals.

Read more about how to use and configure block properties and expressions in [properties](/properties).

## Inputs/Outputs

A block's inputs and outputs are the terminals that receive or send signals and allow interblock interaction. In the System Designer you can connect blocks and allow signals to flow via a block's input and output terminals.

Signals are implemented as dictionaries, a collection of key-value pairs. Signals are always passed between blocks inside of a list.

## Commands

If present, commands can be used to interact with blocks that are part of a running service through the block REST API. Commands are declared in blocks as decorators. Read more about block commands in [api](/api).
