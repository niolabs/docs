# Block Development

The easiest way to create a custom block is to clone the `block-template` repository from `https://github.com/nio-blocks`. This will provide you with the basics of a {{ book.product }} block class as well as the block's requirements, specifications, release notes, and test folder.

## How to Use the Block Template

### Copy the Block Template

1. Navigate to your project's `/blocks` folder.

2. Clone the block template: `git clone --depth=1 https://github.com/nio-blocks/block_template.git <new_block_name>`

2. Navigate into the new block folder: `cd <new_block_name>`

### Rename the Appropriate Files

1. Rename `example_block.py` to the name of your new block.
1. In your new block Python file, rename the `Example` class to the new block's name. Avoid putting `Block` in the class name, this is implied of the filename which should end in `_block.py`
1. Rename `test_example_block.py` to match your new block's class name.
1. Rename `BLOCK_README.md` to `README.md` (`mv BLOCK_README.md README.md`) and update the documentation accordingly.

### Track Your New Block on GitHub

[[ fork from the block template
pull down locally
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

## The {{ book.product }} Framework

 When you develop {{ book.product }} blocks, you use the {{ book.product }} framework. The framework holds all the classes you will be using to create your block and the functionality that ties everything together.

 For example, the first import in `example_block.py` is `nio.block.base`. If you explore inside the `nio.block.base` code, you will find explanatory docstrings for each method, including methods to override in your custom block and higher-level context.

### Block Context

In the configure method, blocks are passed 'context' about themselves and the environment that they are running in. This information is available to be used by block developers:

* **block_router** (BlockRouter):The router in which the block will be running. The only requirements are that it can handle signals notified by its blocks.
* **properties** (dict): The block properties (metadata) that will be deserialized and loaded as block properties.
* **hooks** (Hooks): Hooks to subscribe to participate in the lifecycle process involving all blocks running together.
* **service_name** (str): The name of the service this block belongs to.
* **command_url** (str): The URL at which this block can be commanded. This URL will not have host or port information, as that may be different based on public/private IP. It will look like "/services/ServiceName/BlockAlias/".
* **mgmt_signal_handler** (method): method to use to publish management signals

### Block Router

The block router is what manages the passing of signals from block to block. {{ book.product }} comes packaged with a variety of block routers and each is configurable to control behavior.

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

Stand-alone blocks are discoverable, there is no need for base blocks to be discoverable. If a block does not take in or emit signals, it is non-discoverable.


## Block Patterns

In more complex configurable blocks it is handy to implement a base block pattern. In this pattern, all the configuration that isn't block-specific is done in a non-discoverable base block. The blocks that do the work and process signals will inherit from the base block.

For example, in a block that accesses an external API, you can use a base block to set up the base url then create stand-alone, discoverable blocks to access each specific endpoint in the API. This pattern increases maintainability and reinforces the block philosophy of each block having one unit of functionality.
