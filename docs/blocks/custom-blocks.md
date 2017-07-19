# Custom Blocks

The sky's the limit. If you want to connect to a new framework, library, or custom piece of hardware not currently included in the NIO-blocks collection, you can develop your own custom block.

The basic block philosophy is that one block should do one thing very well. If the piece of functionality you desire is not yet available, it is not difficult to create a custom block.

A {{ book.product }} block is:
- a unit of functionality that runs in a service
- "runnable"—meaning it goes through the nio runnable life cycle: configuring, configured, starting, started, stopping, stopped, (error)
- a functional piece of code that takes input signals and/or emits output signals
- command-able through the block REST API
- a Python class that inherits from nio.block.base.Block
