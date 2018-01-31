# List

The `list` or `ls` command lists all of the blocks or services within a running nio instance.

This command will default for instances running on port 8181. The `-p` flag can be used to list blocks or services from instances on other ports.

Example (blocks):
```bash
nio list blocks
```
returns a list of configured blocks in your running instance
```
Simulate
Log
```

Example (services):
```bash
nio list services
```
returns a list of services in your running instance
```
simulate-and-log
```

Example (port `8282`):
```bash
nio list blocks -p 8282
```
returns a list of blocks in your running instance at port `8282`
