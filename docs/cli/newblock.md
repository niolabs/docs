# New block

The `newblock` command creates a custom block from the official [block template](https://github.com/nio-blocks/block_template) repository. This command clones the project, renames all of the example files, and sets the initial commit for your block.

This command should be run from the `blocks/` directory of your nio project.

Example:
```bash
nio newblock my_block
```
creates a new folder in your current directory named `my_block` containing everything needed to begin developing your custom block.
