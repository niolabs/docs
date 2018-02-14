# Block development

To create a new function or connect to a new framework, library, or custom piece of hardware not currently included in the nio Block Library at [blocks.n.io](https://blocks.n.io/), you can develop your own custom block. To create a custom block, follow the resources here under Block Development as well as the [Develop a Custom Block](https://workshops.n.io/custom-block/) tutorial in workshops.

You can adopt one of two philosophies when creating a block:

  1. Blocks are simple, generic, and reusable. Examples of generic blocks can be found at both the [nio Block Library at blocks.n.io](https://blocks.n.io/) and the [nio-blocks repository on GitHub](https://github.com/nio-blocks). Blocks developed with this approach have a single function and you can chain blocks together to develop complex behaviors.

  2. Blocks can be complex or built for a single use. You would not likely use this block for more than the service it was defined for. For example, a block might contain a script to run a series of calculations for a model. Instead of a complicated chain of blocks, a single block may encompass the entire model. You could also design a single block to parse a Tweet in a unique way that would not be reused.

---

## Add a custom block to the <span class="allow-caps">System Designer</span>

Your custom blocks can be manually installed for local use in the nio System Designer by adding them to your project's `blocks/` directory as a submodule with the
```
git submodule add [repository link]
```
command, and restarting your local nio instance.

---

## Submit your block to the nio <span class="allow-caps">Block Library</span>

Once you have completed, [tested](/blocks/block-development/block-testing.md), and [documented](/blocks/block-development/documenting.md) your block, you can submit your block for approval to the [nio Block Library](https://blocks.n.io) by emailing the block's GitHub repository link to [blocks@n.io](mailto:blocks@n.io).

---

## Create a new block

Begin development of your block with the `nio newblock` command.

Run this command from the `blocks/` directory of your nio project.

```bash
nio newblock <new_block>
```

The nio-cli `newblock` command clones the `block_template` repository at [https://github.com/nio-blocks/block_template](https://github.com/nio-blocks/block_template), renames all of the example files, and sets the initial commit for your new block.

If you need to first create a nio project, use the nio-cli `nio-new` command

```bash
nio new <new_project>
```

For more information about your project directory, refer to the `project_template` repository at <https://github.com/niolabs/project_template>


---

Use the examples provided in [Developing your block](/blocks/block-development/development.md) to guide you in creating your custom block.

---

For a tutorial to step you through block development, go to [workshops.n.io](https://workshops.n.io/custom-block/).
