# Block Development

To get started creating a custom block, clone the `block-template` repository from `https://github.com/nio-blocks`. This will provide you with the basic {{ book.product }} block class as well places for the block's requirements, specifications, release notes, and tests.

## How to Use the Block Template

### Copy the Block Template

1. Navigate into your project's `/blocks` folder. (You can follow the instructions to create a {{ book.product }} project directory here: [First Project](#getting_started/first-project))

2. Clone the block template: `git clone --depth=1 https://github.com/nio-blocks/block_template.git <new_block_name>`

2. Navigate into the new block folder: `cd <new_block_name>`

### Rename the Appropriate Files

1. Rename `example_block.py` to the name of your new block.
1. In your new block Python file, rename the `Example` class to the new block's name. Avoid putting `Block` in the class name, this is implied of the filename which should end in `_block.py`
1. Rename `test_example_block.py` to match your new block's class name.
1. Rename `BLOCK_README.md` to `README.md` (`mv BLOCK_README.md README.md`) and update the documentation accordingly.

### Track Your New Block on GitHub

[[ fork from the block template
pull down locally??
PR?? fork back??? ]]

1. Create a new GitHub repository, often this will have the same name as `<new_block_name>`, and copy the URL
1. Remove the tracking link to the original template repository: `git remote remove origin`
1. Stage your new files: `git add -A`
1. Take ownership: `git commit --amend --reset-author -m "Initial Commit"`
1. Add tracking to your new remote repository: `git remote add origin <new_repo_url>`
1. Push your work to a branch (usually `master`): `git push --set-upstream origin master`

### Block Template File Reference

 * **example_block.py** : This is the block code. Additional Python classes and files are definitely welcome. If the file contains a Block class, make sure the filename ends with `_block.py`. If the file represents a Base Block that is not discoverable by itself, have the filename end with `_base.py`.
 * **requirements.txt** : List out any Python dependencies this block requires. This file will be installed by pip when the block is installed. The command for installing the dependencies is `pip install -r requirements.txt`.
 * **spec.json** : Define the specification for a block, this is the metadata which is used for block discovery.
 * **release.json** : The release data for one or more blocks.
 * **tests/test_example_block.py** : Always submit accompanying unit tests in the `tests` folder.

## Configuring Your Block

A good resource for block development is the {{ book.product }} base block along with blocks with similar functionality that have been developed using the {{ book.product }} framework.

### Base Block Class

All {{ book.product }} blocks inherit from the base block class. You'll notice the first import in `example_block.py`  from your block template is `nio.block.base`. If you explore the code inside `nio.block.base`, you will find explanatory docstrings for each method, including methods to override in your custom block along with higher-level context.

The base block class uses the {{ book.product }} framework described below. Some good things to know about how {{ book.product }} blocks work:
* signals are passed as lists
* block properties need to be called to get the value
* block properties are declared as class attributes
* commands are declared as decorators
* inputs/outputs are declared as decorators

#### Methods to Override

The following method from the base block are designed to be overridden:

* **life cycle management**
  * `configure`: at the end of `configure`, the block is ready to receive signals. If an exception is raised during configure, the service won’t start.
  * `start`: during start, a block can begin to send out signals. This method needs to eventually return so that the block status can change to “started”. For this reason, anything that runs forever (or for a long time), should be done in a new thread.
  * `stop`: tear down. This is where the block stops sending out signals and cancels jobs.
* **signaling**
  * `process_signals(<list of signals>, input_id)`: receives input signals.
  * `notify_signals(<list of signals>, output_id)`: emits signals from the block.

### Current {{ book.product }} Blocks
An additional resource for developing your custom block is the NIO-blocks library. Search the NIO-blocks library for a block that has similar functionality to the block you want to create. Explore the code this block uses, the methods it overrides, and the modules it imports from the framework. These examples will help you develop your block.

### Example: Convert a Python Script to a Block

Here is an example of how to take a Python script and turn it into a block. The developer wanted to use a script that would control a simple motor inside of a {{ book.product }} block.

Python script that controls the motor:
```python
#!/usr/bin/python
#import Adafruit_MotorHAT, Adafruit_DCMotor, Adafruit_Stepper
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

### Block Router

The block router manages the passing of signals from block to block. {{ book.product }} comes packaged with a variety of block routers and each is configurable to control behavior.

#### Configuration

Configuration of block routers is set in the `block_router.cfg` file in the project's `etc/` directory.

* `clone_signals: False`
   * If clone_signals is True, then the block router will perform a deepcopy on the signals whenever they are split and passed to more than one block.
* `max_workers: 50`
   * When using ThreadedPoolExecutorRouter, this is the max number of workers.

#### Block Router Types

Each {{ blook.product }} project can specify a default block router in `nio.conf` by setting block_router.

In addition to specifying the block router for the project, each service can use its own block router by setting block_router on the service configuration.

* **BaseBlockRouter**: Default block router. `nio.router.base.BaseBlockRouter`

* **ThreadedBaseBlockRouter**: Threaded block router. `nio.router.threaded.ThreadedBaseBlockRouter`

* **ThreadedPoolExecutorRouter**: Threaded block router that makes used of thread pools (https://docs.python.org/3/library/concurrent.futures.html). `nio.router.thread_pool_executor.ThreadedPoolExecutorRouter`

### Discoverability

Classes marked as `discoverable` allow the system to identify them and register them, while marking a class as  `not_discoverable` produces the opposite effect. The default state of a block is `discoverable`.

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

## Mixins (?)—here? or elsewhere?
