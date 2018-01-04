# Start nio server

The `server` command starts a nio instance. This command allows nio to be run as a foreground process or it can be run as a background process using the `-d` or `--daemon` command.

```bash
nio server
```
When run from the root of the project directory will start nio. Similar to running `nio_run`.

```bash
nio server -d
```
Will do the same thing but run nio as a background process.
