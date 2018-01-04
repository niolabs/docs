# Add Block

The `add` command adds new blocks to your nio project. These blocks are pulled from the official [nio-blocks GitHub](https://github.com/nio-blocks) repository. All of the requirements for the block will be installed along with it.

This command must be run from the root level of your project. Multiple blocks can also be specified by listing them with spaces.

Example:
```bash
nio add web_handler
```
Will add a the web_handler block submodule under the `blocks/` directory of the project.

```bash
nio add queue debounce
```
Will add both the queue and the debounce block submodules under the `blocks/` directory.
