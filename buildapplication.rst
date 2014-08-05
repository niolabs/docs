Building Your First NIO Application
===================================

Before we get started, let's go over some key concepts that are central to the NIO platform. In this document, we'll discuss **Blocks**, **Signals**, **Services**, the **NIO Core**, and steps you'll need to take in order to build your first NIO app.

Terminology
----------------------------
* **Instance** - A running, well, instance of the NIO executable.
    - Probably comprises multiple **Services**.
* **Service** - The main organizational component in NIO.
    - Each service maintains a **Block execution** that defines connections between some number of blocks.
    - Maintains its own, unique, configuration.
* **Block** - The fundamental unit of computation in NIO.
    - Written in NIO-flavored Python, blocks either operate on **Signals**, interact with the outside world, or both.
* **Signal** - The fundamental unit of data transfer in NIO.
* **Modules** - Uniform API's designed to provide functionality common to many NIO applications without tying developers to any particular library of implementation.
* **Property** - A configurable field on a block or service.
* **Core** - Everything that NIO does that you don't have to worry about.
    - Manages block communication via signals, inter-process communication, block discovery, and much more.


Blocks
------
Here's an example of the most basic possible block, one that accepts incoming signals and passes them along, untouched:

.. code-block:: python

    from nio.common.blocks.base import Block
    from nio.common.discovery import Discoverable, DiscoverableType
    
    @Discoverable(DiscoverableType.block)
    class IDBlock(Block):
    
        def process_signals(self, signals):
    		self.notify_signals(signals)
    		
With no modification, this block will be discovered by a correctly configured NIO service and could run as part of its execution. The core delivers signals notified by other blocks to `IDBlock.process_signals`, where any necessary processing is performed and, optionally, the signals are notified again.

For examples of more complex blocks making use of various modules and higher-order functionality, visit nio_blocks_

.. _nio_blocks: http://github.com/nio-blocks/