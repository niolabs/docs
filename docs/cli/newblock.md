# New Block

The `newblock` command creates a custom block from the official [block template](https;//github.com/nio-blocks/block_template) repository. This command will run through the steps of cloning the project, rename all of the example files, and set the initial commit for your block. 

This command should be run from the `blocks/` directory of your nio project.

Example:
```bash
nio newblock my_block
```
Creates a new folder in your current directory named `my_block` containing everything needed to begin developing your custom nio block.
