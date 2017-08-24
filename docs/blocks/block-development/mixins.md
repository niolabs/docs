# Mixins

Mixins are not blocks. Instead, mixins add commonly used functionality to existing blocks. You can add functions such as persistence, group-by, or retry to blocks. Mixins are shared on GitHub in the [mixin repository](https://github.com/nioinnovation/nio/tree/master/nio/block/mixins).

Mixins follow the Python mixin model, thus any block mixins need to be extended prior to extending the base block class. You can use the persistence and group-by mixins, with the [Buffer block](https://github.com/nio-blocks/buffer).

Make sure you read the docstrings inside each mixin for information on the functionality and arguments.
