# Block Development

To connect to a new framework, library, or custom piece of hardware not currently included in the [nio-blocks repository](https://github.com/nio-blocks), you can develop your own custom block.

You can adopt one of two philosophies when creating a block:

  1. Blocks are simple, generic, and reusable. Examples of generic blocks can be found in the [nio-blocks repository](https://github.com/nio-blocks). Blocks developed with this approach have a single function and you can chain blocks together to develop complex behaviors.

  2. Blocks can be complex or built for a single use. You would not likely use this block for more than the service it was defined for. For example, a block might contain a script to run a series of calculations for a model. Instead of a complicated chain of blocks, a single block may encompass the entire model. You could also design a single block to parse a Tweet in a unique way that would not be reused.

If the function you need does not exist in [the nio-blocks repository](https://github.com/nio-blocks), you can easily create a custom block.

Begin development of your block with the [block template](block-template.md).
