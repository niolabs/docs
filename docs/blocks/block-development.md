# Block Development

To connect to a new framework, library, or custom piece of hardware not currently included in the [nio-blocks library](https://github.com/nio-blocks), you can develop your own custom block.

You can adopt one of two philosophies when creating blocks:

  1. Blocks can be simple, generic, and reusable. Examples of generic blocks can be found in the [nio-blocks repository](https://github.com/nio-blocks). Blocks developed with this approach have a single function and you can chain blocks together to develop complex behaviors.

  2. Blocks can be complex or built for a single use. You would not likely use this block for more than the service it was defined for. For example, a block might contain a script to run a series of calculations for a model. Instead of a complicated chain of blocks, a single block may encompass the entire model. You could also design a single block to parse a Tweet in a unique way that would not be reused.

If the function you need does not exist in [nio-blocks](https://github.com/nio-blocks), you can easily create a custom block.

## Block Template

To create a custom block, clone the [block template repository](https://github.com/nio-blocks/block_template). The block template includes the basic {{ book.product }} block class as well as placeholders for the block's requirements, specifications, release notes, and tests as well as complete instructions in [`README.md`](https://github.com/nio-blocks/block_template).

## Developing Your Block

After downloading the block template repository, you are ready to develop your block.

The {{ book.product }} base block and other blocks with similar functionality that have been developed using the {{ book.product }} framework are good resources for new block development.

As outlined in the [`BLOCK_README.md`](https://github.com/nio-blocks/block_template) file, you have the option to add properties, dependencies, commands, inputs, and outputs to your block.

Before developing your own block, rename the file from `BLOCK_README.md` to `README.md`.
```
mv BLOCK_README.md README.md
```

### Base Block Class

All {{ book.product }} blocks inherit from the base block class. The first import in `example_block.py` from the block template is `nio.block.base`. If you explore the code inside `nio.block.base`, you find explanatory docstrings for each method, including methods to override your custom block along with higher-level context.

The base block class uses the {{ book.product }} framework described below. {{ book.product }} blocks work according to the following principles:
* [Signals](/service-design-patterns/understanding-signals.md) are passed as lists.
* Block properties are declared as class attributes.
```python
speed = IntProperty(title='Speed', default=30)
```
* Block properties must be called with a function invocation to obtain the value. For example, you can get the value of the speed property defined above.
```python
 self.setSpeed(self.speed())
 ```

* Commands are declared as decorators.
  ```python
  from nio.block.base import Block
  from nio.command import command

  @command("emit")
  class MyBlock(Block):
    # properties and block methods here…

    # emit method that will be invoked when the "emit" command is received
    def emit(self, foo=None):
          self._emit_job(foo) # where you have set up your own _emit_job method…
  ```
* Inputs and outputs are declared as decorators.
  ```python
  from nio.block.base import Block
  from nio.block import output

  @output('false', label='False')
  @output('true', label='True')
  class MyBlock(Block):
    # properties and block methods here…

    def process_signals(self, signals):
      true_result, false_result = self._filter_signals(signals) # where you have set up your own _filter_signals method…

      # add any other functionality to process_signals

      self.notify_signals(true_result, 'true')
      self.notify_signals(false_result, 'false')
  ```

#### Methods to Override

The following methods from the base block are designed to be overridden:

* **life cycle management**
  * `configure`: at the end of `configure`, the block is ready to receive signals. If an exception is raised during configure, the service won’t start.
  * `start`: during start, a block begins to send out signals. This method needs to eventually return so that the block status can change to “started”. For this reason, anything that runs continuously, should be run in a new thread.
  * `stop`: after stop, the block stops sending out signals and cancels jobs.
* **signaling**
  * `process_signals(<list of signals>, input_id)`: receives input signals.
  * `notify_signals(<list of signals>, output_id)`: emits signals from the block. This method isn't intended to be overridden, but is it called by the block to send out signals. For example, you will usually call `notify_signals` at the end of your `process_signals` method.

### Current {{ book.product }} Blocks
An additional resource for developing your custom block is the [nio-blocks library](https://github.com/nio-blocks). Search the nio-blocks library for a block that has similar functionality to the block you need. Once you find a block, explore the code, properties, methods, and modules imported from the framework.

## The {{ book.product }} Framework

 When you develop {{ book.product }} blocks, you use the {{ book.product }} framework. The framework holds all the classes required to create your block as well as the functionality to tie everything together. Think of the framework as a toolshed of useful tools for working with {{ book.product }}.

### Block Context

In the configure method, blocks are passed context about themselves and the environment in which they run. Block developers should refer to the following information:

* **block_router** (BlockRouter): The router in which the block runs. The router must be able to handle signals notified by its blocks.
* **properties** (dict): The block properties (metadata) that will be deserialized and loaded.
* **hooks** (Hooks): Hooks are used by the service internally to subscribe to certain overall nio instance lifecycle events. It is not advised to use or rely on these hooks in your blocks.
* **service_name** (str): The name of the service the block belongs to.
* **command_url** (str): The URL at which this block can be commanded. This URL will not have host or port information, as that may be different based on the public/private IP. For example,  "/services/ServiceName/BlockAlias/".
* **mgmt_signal_handler** (method): The method used to publish management signals.

### Discoverability

By default, a class is marked as `discoverable` to permit the system to identify and register the class. Marking a class as `not_discoverable` produces the opposite effect.

To mark a class as not_discoverable, use the parameter-less decorator `@not_discoverable`
```
    from nio import not_discoverable, Block
    @not_discoverable
    class MyBlock(Block):
        pass

```
Base blocks do not need to be discoverable. If a block does not consume or emit signals, include the `@not_discoverable` decorator.

## Base Block Pattern

Implementing a base block pattern is useful in complex configurable blocks. In this pattern, configure the options that are not block-specific in a non-discoverable base block. The blocks that do the work and process signals will inherit from the base block.

For example, in a block that accesses an external API, you can use a base block to set up the base URL, and then create discoverable blocks to access each specific endpoint in the API. A base block pattern is easier to maintain and reinforces the "one function per block" philosophy.

## Mixins

Mixins are not blocks. Instead, mixins add commonly used functionality to existing blocks. You can add functions such as persistence, group-by, or retry to blocks. Mixins are shared on GitHub in the [mixin repository](https://github.com/nioinnovation/nio/tree/master/nio/block/mixins).

Mixins follow the Python mixin model, thus any block mixins need to be extended prior to extending the base block class. You can use the persistence and group-by mixins, with the [Buffer block](https://github.com/nio-blocks/buffer).

Make sure you read the docstrings inside each mixin for information on the functionality and arguments.