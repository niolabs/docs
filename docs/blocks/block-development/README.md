# Block Development

To create a new function or connect to a new framework, library, or custom piece of hardware not currently included in the nio Block Library at [blocks.n.io](https://blocks.n.io/), you can develop your own custom block. To create a custom block, follow the resources here under Block Development as well as the [Develop a Custom Block](https://workshops.n.io/custom-block/) tutorial in workshops.

You can adopt one of two philosophies when creating a block:

  1. Blocks are simple, generic, and reusable. Examples of generic blocks can be found at both the [nio Block Library at blocks.n.io](https://blocks.n.io/) and the [nio-blocks repository on GitHub](https://github.com/nio-blocks). Blocks developed with this approach have a single function and you can chain blocks together to develop complex behaviors.

  2. Blocks can be complex or built for a single use. You would not likely use this block for more than the service it was defined for. For example, a block might contain a script to run a series of calculations for a model. Instead of a complicated chain of blocks, a single block may encompass the entire model. You could also design a single block to parse a Tweet in a unique way that would not be reused.

Begin development of your block with the [block template](block-template.md).

For a tutorial to step you through block development, go to [workshops.n.io](https://workshops.n.io/custom-block/).
