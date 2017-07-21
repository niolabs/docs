# Block Development

The sky's the limit. If you want to connect to a new framework, library, or custom piece of hardware not currently included in the nio-blocks library, you can develop your own custom block.

Block development can adopt one of two philosophies:

  1. Blocks are simple and generic and very reusable. Examples of generic blocks can be found in the [nio-blocks GitHub organization](https://github.com/nio-blocks). Blocks developed with this approach are designed to have a single unit of functionality and you can chain blocks together to get complex behavior.

  2. Blocks can be complex or intended for a single use. This type of block is not likely to be used by more than the one service it was designed for. For example, a block might contain a script to run a series of calculations for a model. Instead of a complicated chain of blocks, a single block can encompasses the entire model. Or a single block might parse a Tweet in a unique way, but not be designed for generic use.

If the type of functionality you desire is not yet available in an existing block, it is not difficult to create a custom block.

To get started creating a custom block, clone the [block-template repository](https://github.com/nio-blocks/block_template) from GitHub. This will provide you with the basic {{ book.product }} block class as well as placeholders for the block's requirements, specifications, release notes, and tests.

Follow the steps in the block template's `README.md`.

## Developing Your Block

Once you have your block template repo, you are ready to develop your block.

A good resource for block development is the {{ book.product }} base block along with blocks with similar functionality that have been developed using the {{ book.product }} framework.

As outlined in your block README (rename it from BLOCK_README.md to README.md: `mv BLOCK_README.md README.md`), you will have the option to add properties, dependencies, commands, inputs, and outputs to your block.

### Base Block Class

All {{ book.product }} blocks inherit from the base block class. You'll notice the first import in `example_block.py` from your block template is `nio.block.base`. If you explore the code inside `nio.block.base`, you will find explanatory docstrings for each method, including methods to override in your custom block along with higher-level context.

The base block class uses the {{ book.product }} framework described below. Some good things to know about how {{ book.product }} blocks work:
* signals are passed as lists ([see more here](/service-design-patterns/understanding-signals.md))
* block properties are declared as class attributes, for example: `speed = IntProperty(title='Speed', default=30)`
* block properties need to be called with a function invocation to get the value, for example to get value the speed property defined above: `self.setSpeed(self.speed())`
* commands are declared as decorators, for example:
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
* inputs/outputs are declared as decorators, for example:
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
  * `start`: during start, a block can begin to send out signals. This method needs to eventually return so that the block status can change to “started”. For this reason, anything that runs forever (or for a long time), should be done in a new thread.
  * `stop`: tear down. This is where the block stops sending out signals and cancels jobs.
* **signaling**
  * `process_signals(<list of signals>, input_id)`: receives input signals.
  * `notify_signals(<list of signals>, output_id)`: emits signals from the block. This method isn't actually intended to be overridden, but is it called by the block to send out signals. For example, you will usually call `notify_signals` at the end of your `process_signals` method.

### Current {{ book.product }} Blocks
An additional resource for developing your custom block is the [nio-blocks library](https://github.com/nio-blocks). Search the nio-blocks library for a block that has similar functionality to the block you want to create. Explore the code this block uses, the properties it has, the methods it overrides, and the modules it imports from the framework.

### Example: Convert a Python Script to a Block

Here is an example of how to take a Python script and turn it into a block. The developer wanted to use a script that would control a simple motor inside of a {{ book.product }} block.

Python script that controls the motor:
```python
#!/usr/bin/python
from Adafruit_MotorHAT import Adafruit_MotorHAT, Adafruit_DCMotor, Adafruit_StepperMotor

import time
import atexit

# create a default object, no changes to I2C address or frequency
mh = Adafruit_MotorHAT()

# recommended for auto-disabling motors on shutdown!
def turnOffMotors():
    mh.getMotor(1).run(Adafruit_MotorHAT.RELEASE)
    mh.getMotor(2).run(Adafruit_MotorHAT.RELEASE)
    mh.getMotor(3).run(Adafruit_MotorHAT.RELEASE)
    mh.getMotor(4).run(Adafruit_MotorHAT.RELEASE)

atexit.register(turnOffMotors)

myStepper = mh.getStepper(200, 1)  # 200 steps/rev, motor port #1
myStepper.setSpeed(30)             # 30 RPM

while (True):
    print("Single coil steps")
    myStepper.step(100, Adafruit_MotorHAT.FORWARD,  Adafruit_MotorHAT.SINGLE)
    myStepper.step(100, Adafruit_MotorHAT.BACKWARD, Adafruit_MotorHAT.SINGLE)

    print("Double coil steps")
    myStepper.step(100, Adafruit_MotorHAT.FORWARD,  Adafruit_MotorHAT.DOUBLE)
    myStepper.step(100, Adafruit_MotorHAT.BACKWARD, Adafruit_MotorHAT.DOUBLE)

    print("Interleaved coil steps")
    myStepper.step(100, Adafruit_MotorHAT.FORWARD,  Adafruit_MotorHAT.INTERLEAVE)
    myStepper.step(100, Adafruit_MotorHAT.BACKWARD, Adafruit_MotorHAT.INTERLEAVE)

    print("Microsteps")
    myStepper.step(100, Adafruit_MotorHAT.FORWARD,  Adafruit_MotorHAT.MICROSTEP)
    myStepper.step(100, Adafruit_MotorHAT.BACKWARD, Adafruit_MotorHAT.MICROSTEP)
```

Python stepper-motor script inside of {{ book.product }} block code:

```python
from nio.block.base import Block
from nio.properties import VersionProperty, IntProperty, SelectProperty

from Adafruit_MotorHAT import Adafruit_MotorHAT, Adafruit_DCMotor, Adafruit_StepperMotor

import time
import atexit
from enum import Enum

class Directions(Enum):
    FORWARD = Adafruit_MotorHAT.FORWARD
    BACKWARD = Adafruit_MotorHAT.BACKWARD

class CoilSteps(Enum):
    SINGLE = Adafruit_MotorHAT.SINGLE
    DOUBLE = Adafruit_MotorHAT.DOUBLE
    INTERLEAVE = Adafruit_MotorHAT.INTERLEAVE
    MICROSTEP = Adafruit_MotorHAT.MICROSTEP

class StepMotor(Block):

    version = VersionProperty('0.1.0')
    motor = IntProperty(title='Motor number', default=1)
    steprate = IntProperty(title='Step Rate', default=200)
    speed = IntProperty(title='Speed', default=30)
    steps = IntProperty(title='Number of Steps', default=100)
    direction = SelectProperty(Directions, title="Direction", default="FORWARD")
    coil_steps = SelectProperty(CoilSteps, title="Coil Steps", default="SINGLE")

    def __init__(self):
        super().__init__()
        self.mh = None
        self.stepper = None

    def turnOffMotors(self):
        self.mh.getMotor(1).run(Adafruit_MotorHAT.RELEASE)
        self.mh.getMotor(2).run(Adafruit_MotorHAT.RELEASE)
        self.mh.getMotor(3).run(Adafruit_MotorHAT.RELEASE)
        self.mh.getMotor(4).run(Adafruit_MotorHAT.RELEASE)

    def start(self):
        self.mh = Adafruit_MotorHAT()
        atexit.register(self.turnOffMotors)
        self.stepper = self.mh.getStepper(self.steprate(), self.motor())
        self.stepper.setSpeed(self.speed())

    def process_signals(self, signals):
        for signal in signals:
            self.stepper.step(self.steps(), self.direction().value,  self.coil_steps().value)
        self.notify_signals(signals)
```

## The {{ book.product }} Framework

 When you develop {{ book.product }} blocks, you use the {{ book.product }} framework. The framework holds all the classes you will be using to create your block as well as the functionality that ties everything together. Think of the framework as a toolshed of useful tools for working with {{ book.product }}.

### Block Context

In the configure method, blocks are passed 'context' about themselves and the environment that they are running in. This information is available to be used by block developers:

* **block_router** (BlockRouter):The router in which the block will be running. The only requirements are that it can handle signals notified by its blocks.
* **properties** (dict): The block properties (metadata) that will be deserialized and loaded as block properties.
* **hooks** (Hooks): Hooks to subscribe to participate in the lifecycle process involving all blocks running together.
* **service_name** (str): The name of the service this block belongs to.
* **command_url** (str): The URL at which this block can be commanded. This URL will not have host or port information, as that may be different based on public/private IP. It will look like "/services/ServiceName/BlockAlias/".
* **mgmt_signal_handler** (method): method to use to publish management signals

### Discoverability

Classes marked as `discoverable` allow the system to identify them and register them, while marking a class as `not_discoverable` produces the opposite effect. The default state of a block is `discoverable`.

To mark a class as not_discoverable, use the parameter-less decorator `@not_discoverable`
```
    from nio import not_discoverable, Block
    @not_discoverable
    class MyBlock(Block):
        pass

```
There is no need for base blocks to be discoverable. If a block does not take in or emit signals, it should include the `@not_discoverable` decorator.

## Base Block Pattern

In more complex configurable blocks it is handy to implement a base block pattern. In this pattern, all the configuration that isn't block-specific is done in a non-discoverable base block. The blocks that do the work and process signals will inherit from the base block.

For example, in a block that accesses an external API, you can use a base block to set up the base url then create discoverable blocks to access each specific endpoint in the API. This pattern increases maintainability and reinforces the philosophy of each block having one unit of functionality.

## Mixins

Extend mixins to add functionality such as persistence, group-by, and retry to your blocks. You'll find some mixins in `nio.block.mixins`.

Mixins are not blocks, they are meant to enhance blocks by providing commonly used functionality.

Because these follow the Python mixin model, any block mixins will need to be extended before extending the base Block class. See the [Buffer block](https://github.com/nio-blocks/buffer) for examples of how to use the persistence and group-by mixins.

Docstrings inside each mixin give more information about their respective arguments and functionality.
