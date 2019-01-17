# Mixins

Mixins are not blocks. Instead, mixins add commonly used functionality to existing blocks. You can add functions such as `persistence`, `group-by`, or `retry` to blocks. Mixins are shared on GitHub in the [mixin repository](https://github.com/niolabs/nio/tree/master/nio/block/mixins).

Mixins follow the Python mixin model, thus any block mixins need to be extended prior to extending the base block class. You can see an example of using the persistence and group-by mixins in the [_Buffer_](https://github.com/nio-blocks/buffer) block.
```py
from nio.block.base import Block
from nio.block.mixins import Persistence, GroupBy

class Buffer(Persistence, GroupBy, Block):

```

Docstrings inside each mixin provide more information on each mixin's functionality and arguments.

The following mixins are currently available in the nio framework for use in your block code:

 * [Collector](/blocks/block-mixins/collector.md) -  Collect or buffer signals before notifying them.
 * [EnrichSignals](/blocks/block-mixins/enrich-signals.md) - Enrich incoming signals with new data from a block
 * [GroupBy](/blocks/block-mixins/group-by.md) - Allow your block to operate independently on groups of signals in a single stream
 * [LimitLock](/blocks/block-mixins/limit-lock.md) - Lock operations across threads with a capped queue of threads waiting to acquire the lock
 * [Persistence](/blocks/block-mixins/persistence.md) - Save data from your block to handle service and instance restarts or crashes
 * [Retry](/blocks/block-mixins/retry.md) - Retry operations that may fail with a configurable backoff strategy

