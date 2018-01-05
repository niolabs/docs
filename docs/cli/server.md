# Start nio server

The `server` command starts a nio instance. This command allows nio to be run as a foreground process or it can be run as a background process using the `-d` or `--daemon` command.

This command must be run from the root level of your project directory.

```bash
nio server
```
This command is similar to running `niod`.

```bash
nio server -d
```
Does the same thing but runs nio as a background process.
