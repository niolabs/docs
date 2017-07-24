# Block Development

The sky's the limit. To connect to a new framework, library, or custom piece of hardware not currently included in the nio-blocks library, you can develop your own custom block.

You can adopt one of two philosophies when creating blocks:

  1. Blocks can be simple, generic, and reusable. Examples of generic blocks can be found in the [nio-blocks GitHub organization](https://github.com/nio-blocks). Blocks developed with this approach have a single function and and you can chain blocks together to develop complex behaviors.

  2. Blocks can be complex or built for a single use. You would not likely use this block for more than the service it was defined for.  For example, a block might contain a script to run a series of calculations for a model. Instead of a complicated chain of blocks, a single block may encompass the entire model. You could also design  a single block to parse a Tweet in a unique way that would not be reused.

If the function you need does not exist in [nio-blocks](https://github.com/nio-blocks), you can easily create a custom block.

To create a custom block, clone the [block-template repository](https://github.com/nio-blocks/block_template) from GitHub. The block template includes the basic {{ book.product }} block class as well as placeholders for the block's requirements, specifications, release notes, and tests.

See the [`README.md`](https://github.com/nio-blocks/block_template)  for complete instructions. 

## Developing Your Block

After downloading the block template repository, you are ready to develop your block.

The {{ book.product }} base block and blocks with similar functionality that have been developed using the {{ book.product }} framework are good resources for block development.

As outlined in your block readme file, you have the option to add properties, dependencies, commands, inputs, and outputs to your block. 

Before developing your own block, rename the block from  BLOCK_README.md to README.md by executing the following command: 
`mv BLOCK_README.md README.md`

### Base Block Class

All {{ book.product }} blocks inherit from the base block class. The first import in `example_block.py` from the block template is `nio.block.base`. If you explore the code inside `nio.block.base`, you find explanatory docstrings for each method, including methods to override in your custom block along with higher-level context.

The base block class uses the {{ book.product }} framework described below. {{ book.product }} blocks work according the following principals:
* Signals are passed as lists. See [Understanding Signals](/service-design-patterns/understanding-signals.md).
* Block properties are declared as class attributes. 
For example, `speed = IntProperty(title='Speed', default=30)`
* Block properties must be called with a function invocation to obtain the value. For example to get value the speed property defined above, call `self.setSpeed(self.speed())`
* Commands are declared as decorator. 
For example:
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
* Inputs/outputs are declared as decorators. 
For example:
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

The following methods from the base block are designed to be overridden: //Matt: do you mean overwritten?//

* **life cycle management** //matt: is this a command you run? where? does this cover the 6 step life cycle (starting, started, etc)//
  * `configure`: at the end of `configure`, the block is ready to receive signals. If an exception is raised during configure, the service won’t start.
  * `start`: during start, a block begins to send out signals. This method needs to eventually return so that the block status can change to “started”. For this reason, anything that runs continuously, should be run in a new thread.
  * `stop`: after top, the block stops sending out signals and cancels jobs.
* **signaling**
  * `process_signals(<list of signals>, input_id)`: receives input signals.
  * `notify_signals(<list of signals>, output_id)`: emits signals from the block. This method isn't intended to be overridden, but is it called by the block to send out signals. For example, you will usually call `notify_signals` at the end of your `process_signals` method.

### Current {{ book.product }} Blocks //Matt: Is there a name for "standard" blocks instead of current? Core blocks? ??//
An additional resource for developing your custom block is the [nio-blocks library](https://github.com/nio-blocks). Search the nio-blocks library for a block that has similar functionality to the block you need. Once you find a block, explore the code, properties, methods, and modules imported from the framework.

### Example: Convert a Python Script to a Block //Matt: are these steps complete?//

The developer wants to use a script to control a simple motor inside of a {{ book.product }} block. To convert a Python script to a block:

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

 When you develop {{ book.product }} blocks, you use the {{ book.product }} framework. The framework holds all the classes required to create your block as well as the functionality to tie everything together. Think of the framework as a toolshed of useful tools for working with {{ book.product }}.

### Block Context

In the configure method, blocks are passed 'context' about themselves and their. Block developers should refer to the following information:

* **block_router** (BlockRouter): The router in which the block will be run. The router must be able to handle signals notified by its blocks.
* **properties** (dict): The block properties (metadata) that will be deserialized and loaded.
* **hooks** (Hooks): Hooks to subscribe to participate in the lifecycle process involving all blocks running together. //Matt: Alternate: not sure what this means//
* **service_name** (str): The name of the service this block belongs to.
* **command_url** (str): The URL at which this block can be commanded. This URL will not have host or port information, as that may be different based on public/private IP. For example,  "/services/ServiceName/BlockAlias/".
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
Base blocks do not need to be discoverable. If a block does not consume or emit signals, include the `@not_discoverable` decorator. //Matt: earlier we said that all blocks take signals in or out--what about transforms?//

## Base Block Pattern

Implementing a base block pattern is useful in complex configurable blocks. In this pattern, configure the options that are not block-specific in a non-discoverable base block. The blocks that do the work and process signals will inherit from the base block.

For example, in a block that accesses an external API, you can use a base block to set up the base url then create discoverable blocks to access each specific endpoint in the API. A base block pattern is easier to maintain and reinforces one-function-per block philosophy.

## Mixins

Mixins are not blocks. Instead, mixins provide commonly used functionality to existing blocks. You can add functions such as persistence, group-by, or retry to blocks. You can find some mixins in `nio.block.mixins`. //Matt: where is this? I've found two mixins in the nio-blocks repository?? https://github.com/nioinnovation/nio/tree/master/nio/block/mixins//

Mixins follow the Python mixin model, thus any block mixins need to be extended prior to extending the base Block class. To use persistence and group-by mixins, see [Buffer block](https://github.com/nio-blocks/buffer).

Read the docstrings inside each mixin for information on the functionality and arguments.
