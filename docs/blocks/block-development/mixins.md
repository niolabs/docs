# Mixins

Mixins are not blocks. Instead, mixins add commonly used functionality to existing blocks. You can add functions such as `persistence`, `group-by`, or `retry` to blocks. Mixins are shared on GitHub in the [mixin repository](https://github.com/niolabs/nio/tree/master/nio/block/mixins).

Mixins follow the Python mixin model, thus any block mixins need to be extended prior to extending the base block class. You can see an example of using the persistence and group-by mixins in the [_Buffer_ block](https://github.com/nio-blocks/buffer).
```py
from nio.block.base import Block
from nio.block.mixins import Persistence, GroupBy

class Buffer(Persistence, GroupBy, Block):

```

Docstrings inside each mixin provide more information on each mixin's functionality and arguments.
