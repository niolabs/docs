# Documenting your block

There is a preferred way to document a nio Block, if you started by using the [Block Template](https://github.com/nio-blocks/block_template) the recommended file structure is already in place and you only need to write a helpful README. For more information on using Markdown, see the official [guide on GitHub](https://guides.github.com/features/mastering-markdown/). If you would like to submit your block to the [nio blocks library](https://blocks.n.io) for public use please [send us a message](mailto:blocks@n.io) with a link to your repository!

## Create or modify the following files:
### README.md
This file is targeted to developers, listing any extra installation requirements, dependencies, or other information that a user may need to get these blocks working.

**Style Guide:**
A root-level readme should always include at least two sections: *Blocks in this collection* and *Dependencies*. Other sections such as *Notes* and *Installation* may be included as necessary. Section headers should be size H2 (start a line with `##`), and list each value under it on a new line. For example:

```
## Blocks in this Collection
  - (Example)[docs/example_block.md]

## Dependencies
None
```

### docs/example_block.md
Create one file like this for every block included in this repository. This file should include all of the configurable properties and commands for the block, as well as examples of its use. Users will reference this file while building services, for non-custom blocks this is the file displayed in block help windows and the nio blocks library. Examples should illustrate the block's operation given a variety of configurations and conditions.

**Style Guide:**
Block readmes should begin with the block's name as an H1 header (line starts with `#`). This is the name of the block's defining class, and the name displayed on blocks inside the System Designer. Include a section for *Properties*, *Advanced Properties*, and *Commands* as necessary (again, all size H2).
