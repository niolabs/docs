# Update Block

The `update` subcommand command is very simple but very important. It compels a running NIO instance to rediscover each of the block types in its argument list, allowing developers to perform live updates to block implementations. For example, after updating the implementation for the LoggerBlock:

```
    $ nio update Logger
```
If all the block types are valid, standard out should remain silent.
NB: The current implementations of a running block will remain in memory until the enclosing service is restarted.

--------
The `update` command (Isn't really a thing..)
