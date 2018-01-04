# Clone Services

The `clone services` command will create a copy of one service configuration.

Example:
```bash
nio clone service simulate-and-log simulate-and-log2
```
Will create a second service `simulate-and-log2` which will have the exact same blocks and configuration as `simulate-and-log`. This can be checked by viewing the services in the System Designer or by running `nio list services`.
