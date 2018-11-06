# Publishing your block

The nio CLI allows you to publish blocks to the [nio Block Repository](https://blocks.n.io) using the `publishblock` command.

>**[info] Block Publishing Permission**
>
> Publishing blocks is currently restricted to certified block publishers. If you'd like to publish a block and do not have this certification, contact *info@n.io* to inquire.

## Basic Functionality

The *publishblock* command is intended to be run from the root of a block repository. It depends on finding a *spec.json* and *release.json* for the block in that folder.

In most cases the command will inquire the block code to determine the block's properties, commands, version, etc. You can see the spec and release that will be published to the nio Block Repository by using the `--dry-run` flag. This will not send any information to the API

```bash
nio publishblock --dry-run
```

When you have confirmed the spec and release look good and are ready to publish, set your API access token (JWT) to the `API_ACCESS_TOKEN` environment variable and run the command

```bash
export API_ACCESS_TOKEN=your_token_goes_here
nio publishblock
```

### Additional Arguments

The following arguments can be passed to the `nio publishblock` command:

 * *--dry-run* - Don't publish anything, instead print the determined spec and releases
 * *--api-token* - The JWT for the API to authenticate. You can also use the `API_ACCESS_TOKEN` environment variable for this.
 * *--api-url* - The root of the API URL to hit. Defaults to the production block API `https://api.n.io/v1/block`

## Specification for spec.json

The *spec.json* file should be a valid JSON file that contains a map of block names to block specs. Each block name must be namespaced. The spec.json file should have a block spec for every block that is present in the given repository.

The following options can be provided the spec object:

 * *description* - (required) - A brief (<4000 character) description of what the block does
 * *categories* - (required) - A list of block categories
 * *from_python* - A Python file where the block information can be sourced
 * *from_readme* - A markdown file where the long desctiption can be sourced
 * *long_description* - A longer description of the block's behavior. Markdown is supported (can be inferred using from_readme)
 * *properties* - A mapping of the block's properties (can be inferred using from_python)
 * *commands* - A mapping of the block's commands (can be inferred using from_python)
 * *inputs* - A mapping of the block's inputs (can be inferred using from_python)
 * *outputs* - A mapping of the block's outputs (can be inferred using from_python)
 * *version* - The version of the block spec (can be inferred using from_python)

### The from_python property

A block spec can contain a special property called `from_python` that represents a Python file and class. The format of this property should be `path.to.python_file.PythonClass` where `path.to.python_file` represents the Python namespace, relative to the `spec.json` file, where the class can be loaded from. `PythonClass` should be the class name of the block.

For example, if you have a block class defined in `classes/sample_block.py` called `SampleBlock`, then your `from_python` value would look like `classes.sample_block.SampleBlock`. Note the removal of the `.py` suffix.

There is no need to add the project to your PYTHONPATH, this will be done automatically in the CLI.

### Example spec.json
```
{
  "nio/SampleBlock": {
    "description": "A fake block",
	"categories": ["Signal Modifier"],
	"from_python": "sample_block.SampleBlock",
	"from_readme": "README.md"
  }
}
```

## Specification for release.json

The *release.json* file should be a valid JSON file that contains a map of block names to block release information. Each block name must be namespaced. The release.json file should have a block spec for every block that is present in the given repository.

The following options can be provided the release information object:

 * *language* - (required) - The language the block is written in (e.g., Python)
 * *url* - (required) - A git URL where the block can be downloaded (e.g., `git://github.com/fake/block.git`). Be sure to use the `git://` format of the URL and not `https://` or `git@`.
 * *from_python* - A Python file where the block information can be sourced. See the documentation above for usage of this property.
 * *version* - The version of the block release (can be inferred using from_python)

### Example release.json
```
{
  "nio/SampleBlock": {
    "language": "Python",
	"from_python": "sample_block.SampleBlock",
	"url": "git://github.com/nio-blocks/sample.git"
  }
}
```

## Example CLI usage

```bash
export API_ACCESS_TOKEN=your_jwt_goes_here
nio publishblock
```
Publishes the blocks in your repository to the nio Block Repository

```bash
nio publishblock --dry-run
```
Prints to the screen the spec and release of the block. Use this to confirm your files are correct
