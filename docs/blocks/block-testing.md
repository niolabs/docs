# Block Testing

{{ book.product }} blocks are not meant to be run as stand-alone Python modules, so testing can be a challenging process. n.io provides a couple of tools and offers best practices to make your testing easier.

## NIOBlockTestCase

When building your tests, use the `NIOBlockTestCase`. The test case extends `unittest.TestCase` and uses the same infrastructure as the base class. However, `NIOBlockTestCase` also provides a number of helpful methods for testing blocks. Here's a real-world example from our internal block repositories:

```python

from nio.testing.block_test_case import NIOBlockTestCase
from nio.signal.base import Signal
from ..your_block import YourBlock

class TestYourBlock(NIOBlockTestCase):

	 def test_some_feature(self):
		 blk = YourBlock()
		 self.configure_block(blk, {
			 'int_prop': 23,
			 'obj_prop': {
				 'p1': 'foo',
				 'p2': 'bar'
			 }
		 })
		 blk.start()
		 blk.process_signals([Signal()])
		 blk.stop()
		 # your assertions here…

 ```

## setUp/tearDown

Just like `unittest.TestCase`, we support the setUp/tearDown pattern. This is a great place to do any initialization and/or cleanup that will be required across every test. Do not repeat yourself! Be aware, though, that the block provides crucial initialization and finalization in `NIOBlockTestCase.setUp/tearDown`. If you override either of these methods, you need to call the method in the parent class at the top of your method.

## Helper Methods

- **configure_block(block, block_properties)** - The process of configuring and initializing blocks manually is somewhat nuanced (and not something we want you to worry about). We provide this method to configure your block instance semi-automatically. Just pass the block object itself and a dictionary containing any block properties you want to configure (and associated values).
- **assert_num_signals_notified(num, block=None)** - This method provides access to the total number of signals notified over the course of the current test. If `block` is not `None`, then you will receive the number of signals notified by that block over its lifetime.
- **last_signal_notified(output_id)** - This method returns the last signal that was notified from a particular output. If an output_id is not specified, it will return the last signal notified from any output on the block.

## Overridable Methods

-   **get_test_modules()** - By default, `NIOBlockTestCase` automatically initializes the logging, threading, scheduler, and security modules. However, you can customize this by overriding this method and returning a list of strings corresponding to the particular modules you want to initialize. Your options are as follows:
    * logging
    * threading
    * scheduler
    * security
    * communication
    * persistence
    * web
-   **signals_notified(signals, output_id)** - This method gets called every time signals are notified in your tests. If you'd like to record something in the test case, trigger an event, or perform some aggregation when that happens, override this method. One common use is to add `self.signals = defaultdict(list)` to `setUp` and:

```python
def signals_notified(self, signals, output_id):
	self.signals[output_id].extend(signals)
```

## Events

This is more a best practice than a feature. Blocks are not required to behave synchronously, and sometimes you may want to wait for an event (after instantiating or configuring a block) before proceeding with the tests. Rather than sleeping for a prescribed amount of time (asynchronous processes can be fickle and unpredictable from machine to machine), we recommend extending the block and adding one of Python's Event objects to signify readiness. For example:

```python
class EventBlock(YourBlock):
	def __init__(self, event):
		super().__init__()
		self.e = event

	def configure(self, context):
		super().configure(context)
		self.e.set()
```

Now, instead of instantiating `YourBlock` in the tests, instantiate `EventBlock` passing an instance of `Event` to its constructor. Fox example:

```python
from threading import Event
e = Event()
blk = EventBlock(e)
self.configure_block(blk, {'p1': 23})
e.wait(2)
```

Using the `EventBlock`, your test will wait until  `YourBlock.configure` returns control to the method on the child class. Your test will never proceed until `EventBlock.e` is set.

## Mocking

Patching and mocking are extremely useful concepts in software verification; this is especially relevant when the modules in question interact with external resources (such as APIs, OS services, and so on). We won't go into too much details of mocking right now, but the [Python documentation](https://docs.python.org/3/library/unittest.mock.html) contains great material on the subject. We recommend using these concepts liberally; in fact, in many cases you won't have much choice.

As you progress, one thing you may notice is that `unittest.mock.patch` doesn't play nice with relative module paths. This makes patching a method at the class or module level difficult.  One solution is to import the object directly and use `unittest.mock.patch.object`

```python
from unittest.mock import patch, ANY
from ..queue_block import Queue

@patch.object(Queue, '_load')
def test_it(self, load_patch):
	...
	load_patch.assert_called_once_with(ANY)
```
Again, you don't necessarily have to construct your tests in this manner; however, we've found this practice to be more convenient and less prone to user error than others.

## Mocking Persistence Module

To mock `load` the persistence module:

```python
class TestPersistenceBlock(NIOBlockTestCase):

	def test_persist_load(self):
		blk = Block()
		with path('nio.modules.persistence.default.Persistence.load') as load:
			load.return_value = 'i was persisted'
			self.configure_block(blk, {})
```
To mock `store` and `save`:

```python
from unittest.mock import  MagicMock

class TestPersistenceBlock(NIOBlockTestCase):

	def test_persist_save(self):
		 blk = Block()
		 self.configure_block(blk, {})
		 blk.persistence.store = MagicMock()
		 blk.persistence.save = MagicMock()
```

## {{ book.product }} Modules

`NIOBlockTestCase` configures the following {{ book.product }} modules by default: `['logging', 'scheduler', 'security', 'threading']`. If your block test case needs to use any other {{ book.product }} modules, you must specify by implementing the `get_test_modules` method.

For example, if your test case uses persistence:

```python
class TestBlock(NIOBlockTestCase):

	def get_test_modules(self):
		return super().get_test_modules() + ['persistence']
```
You can override the default configuration of modules by implementing `get_module_config_*`. The following example will ensure that the test case uses the `default` implementation of the persistence module.

```python
class TestBlock(NIOBlockTestCase):

	def get_module_config_persistence(self):
		return {'persistence': 'default'}
```
