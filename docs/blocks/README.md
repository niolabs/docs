# Blocks

A {{ book.product }} block is:
- a unit of functionality that runs in a service
- "runnable"—meaning it goes through the nio runnable life cycle: configuring, configured, starting, started, stopping, stopped, (error)
- a functional piece of code that takes streaming input signals and/or emits streaming output signals
- command-able through the block REST API
- a Python class that inherits from `nio.block.base.Block`
