# Custom Blocks

The sky's the limit. If you want to connect to a new framework, library, or custom piece of hardware not currently included in the nio-blocks library, you can develop your own custom block.

Block development can take one of two approaches:

1. Blocks are simple and generic and very reusable. Examples of generic blocks can be found in the [nio-blocks GitHub organization](https://github.com/nio-blocks). Blocks developed with this approach are meant to have a single unit of functionality and you can chain blocks together to get complex behavior.

2. Blocks can be extremely custom and meant for a single purpose. This type of block is not likely to be used by more than the one service it was designed for.

If the type of functionality you desire is not yet available in an existing block, it is not difficult to create a custom block.

A {{ book.product }} block is:
- a unit of functionality that runs in a service
- "runnable"—meaning it goes through the nio runnable life cycle: configuring, configured, starting, started, stopping, stopped, (error)
- a functional piece of code that takes streaming input signals and/or emits streaming output signals
- command-able through the block REST API
- a Python class that inherits from `nio.block.base.Block`
