# Persistence with nio

Certain block types, such as [_StateChange_](https://blocks.n.io/StateChange), [_Buffer_](https://blocks.n.io/Buffer), and [_Sleep_](https://blocks.n.io/Sleep), give the user an option to "Load from Persistence."

<!-- TODO: add image of load from persistence prop -->

This [block mixin](/blocks/block-development/mixins.html) gives a block the ability to save its current data to disk when the parent service is stopped and to load that data when started. Without this function, data or state within the block would be lost when the service stops.

The data saved depends on the block type, but generally allows a block to start where it left off when it was last stopped. This may include the current state evaluation, the contents of a buffer, or a scheduled task. Persistence is not a storage solution, but a method of handling interruptions to a running system.

<!-- TODO: insert figure 1 image – should this go through design? -->

In the above example, a [_Sleep_](https://blocks.n.io/Sleep) block loads from persistence after an interruption and continues with its scheduled tasks. Without this function, or if the service was not restarted before the end of the sleep interval, the signal received would have been dropped and never notified.

<!-- TODO: insert figure 2 – should this go through design? -->

This timeline shows how a [_StateChange_](https://blocks.n.io/StateChange) evaluation that is loaded from persistence does not notify a signal after restarting, because the state evaluation is the same as it was when stopped. The next signal where `x > 0` will evaluate to "True" and be notified normally. If not loaded from persistence, the second signal with `x = 0` would have evaluated "False" and also notified a signal. Depending on your application and system, this repetition of a "False" state may or may not be desirable.

### Using Persistence in your own Blocks

Maybe you've built a custom block that you want to survive instance and service restarts. The persistence module in the nio framework is ultimately what is responsible for persisting data from blocks. However, the nio framework also includes a [handy mixin](https://github.com/niolabs/nio/tree/master/nio/block/mixins/persistence) to make this easier for block developers. Use of this mixin is the recommended way to add persistence to your custom blocks.

<!-- TODO: add "Read more about how to use the Persistence mixin [here](link)" when docs are ready -->
