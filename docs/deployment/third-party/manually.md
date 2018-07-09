# With command line and `git`

There are a few steps in a local install of the nio binary that can be done manually instead of using the nio CLI functionality that has been built into the nio Platform for you.

---

## Download a nio project template using `git`
To download the project template using Git, clone the template and initialize the submodules, which contain the default blocks, using the following commands:
```
git clone https://github.com/niolabs/project_template.git first_project
cd first_project
git submodule update --init --recursive
```

---

## Add blocks from the command line
In addition to adding blocks from within the nio System Designer, you can add blocks to your instance directly from the command line.

From the project root directory, add the relevant block repository into the `blocks/` folder. For example, the _Logger_ block:
```
nio add logger
```

You can also add a block to your project using Git. From the `blocks/` directory in your project, enter the following command:
```
git submodule add https://github.com/nio-blocks/logger.git
```

Learn more about how to configure blocks and connect them to perform various nio services in the tutorials at https://workshops.n.io/.
