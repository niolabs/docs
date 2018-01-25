# Persistence with the nio Platform

Certain nio Block types, such as [_StateChange_](https://blocks.n.io/StateChange), [_Buffer_](https://blocks.n.io/Buffer), and [_Sleep_](https://blocks.n.io/Sleep), give the user an option to "Load from Persistence".

The persistence block [mixin](/blocks/block-development/mixins.html) uses the persistence module to give a block the ability to save its current data to disk when the parent service is stopped and to load that data when started. Without this function, data or state within the block would be lost when the service stops.

The data saved depends on the block type, but generally allows a block to start where it left off when it was last stopped. This may include the current state evaluation, the contents of a buffer, or a scheduled task. Persistence is not a storage solution, but a method of handling interruptions to a running system.

<img class="border display" src="/img/persistence1.png" width="500" />

In the above example, a [_Sleep_](https://blocks.n.io/Sleep) block loads from persistence after an interruption and continues with its scheduled tasks. Without this function, or if the service was not restarted before the end of the sleep interval, the signal received would have been dropped and never been sent.

<img class="border display" src="/img/persistence2.png" width="500" />

This timeline shows how a [_StateChange_](https://blocks.n.io/StateChange) evaluation that is loaded from persistence does not emit a signal after restarting, because the state evaluation is the same as it was when stopped. The next signal where <br>`x > 0` will evaluate to "True" and be emitted normally. If not loaded from persistence, the second signal with `x = 0` would have evaluated "False" and also output a signal. Depending on your application and system, this repetition of a "False" state may or may not be desirable.

---

## Persistence mixin

The persistence module in the nio framework is ultimately responsible for persisting data from blocks through instance and service stops and restarts. However, for block developers, the nio framework includes a handy [mixin](https://github.com/niolabs/nio/tree/master/nio/block/mixins/persistence) to add persistence to blocks. Use the persistence [mixin](https://github.com/niolabs/nio/tree/master/nio/block/mixins/persistence) when you want to easily add persistence to your custom block.

<!-- TODO: add "Read more about how to use the Persistence mixin [here](link)" when docs are ready -->
