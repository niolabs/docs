# The nio Framework

When you develop blocks, you use the nio framework. The framework holds all the classes required to create your block as well as the functionality to tie everything together. Think of the framework as a toolshed of useful tools and context for working with the nio Platform.

---

## Block Context

In the configure method, blocks are passed context about themselves and the environment in which they run. Block developers should refer to the following information:

* **block_router** (BlockRouter): The router in which the block runs. The router must be able to handle signals emitted by its blocks.
* **properties** (dict): The block properties (metadata) that will be deserialized and loaded.
* **hooks** (Hooks): Hooks are used by the service internally to subscribe to certain overall nio instance lifecycle events. It is not advised to use or rely on these hooks in your blocks.
* **service_name** (str): The name of the service the block belongs to.
* **command_url** (str): The URL at which this block can be commanded. This URL will not have host or port information, as that may be different based on the public/private IP. For example,  "/services/ServiceName/BlockAlias/".
* **mgmt_signal_handler** (method): The method used to publish management signals.

---

## Discoverability

By default, a class is marked as `discoverable` to permit the system to identify and register the class. Marking a class as `not_discoverable` produces the opposite effect.

To mark a class as not_discoverable, use the parameter-less decorator `@not_discoverable`.
```
    from nio import not_discoverable, Block
    @not_discoverable
    class MyBlock(Block):
        pass

```
Base blocks do not need to be discoverable. If a block does not consume or emit signals, include the `@not_discoverable` decorator.
