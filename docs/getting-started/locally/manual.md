# Manual Installation

There are a few steps in a local install of the nio binary that can be done manually instead of using functionality that has been built into the nio Platform for you.

## Download a nio Project Template Using Git
To download the project template using Git, clone the template and initialize the submodules, which contain the blocks, using the following commands:
```
git clone https://github.com/niolabs/project_template.git first_project
cd first_project
git submodule update --init --recursive
```

## Add Blocks Manually
In addition to adding blocks from within the nio System Designer, you can add blocks to your instance directly from the command line.

From the project root directory, add the relevant block repository into the `blocks/` folder. For example, the logger block:
```
nio add logger
```

You can also add a block to your project using Git. From the `blocks/` directory in your project, enter the following command:
```
git submodule add https://github.com/nio-blocks/logger.git blocks/logger
```

Learn more about how to configure blocks and connect them to perform various services in the tutorials at https://workshops.n.io/.

## Upgrade the nio binary and CLI

If you already have a version of nio installed and want to upgrade it, enter the following command:
```
pip3 install -U your_wheel_file.whl
```
