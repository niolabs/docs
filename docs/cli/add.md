# Add Block

The `add` command adds new blocks to your nio project. The block code is pulled from the official [nio-blocks GitHub](https://github.com/nio-blocks) repository. The command installs all of the requirements for the block along with the block.

This command must be run from the root level of your project directory.

Multiple blocks can be specified by listing them with spaces.

Example:
```bash
nio add web_handler
```
adds the _WebHandler_ block submodule under the `blocks/` directory of the project.

```bash
nio add queue debounce
```
adds both the _Queue_ and the _Debounce_ block submodules under the `blocks/` directory.
