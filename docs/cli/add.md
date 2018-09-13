# Add block

The `add` command adds new blocks to your running nio instance. The block code is pulled from the official [nio-blocks GitHub](https://github.com/nio-blocks) repository. The command installs all of the requirements for the block along with the block through the project management component.

This command must be run for a running nio instance. `--port`, `--username`, and `--password` options should be used for non standard configured nio instances.

Multiple blocks can be specified by listing them with spaces.

---

## Example:

```bash
nio add web_handler
```
installs the _WebHandler_ block to a running nio instance.

```bash
nio add queue debounce
```
installs both the _Queue_ and the _Debounce_ blocks to a running nio instance.

```bash
nio add slack --port 8182 --username foo --password bar
```
installs the _Slack_ block to a running nio instance at NIOPORT 8182 with an authorized instance user "foo".
