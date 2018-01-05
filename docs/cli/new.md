# New Project

The `new` command creates a fresh project from the official [project template](https;//github.com/niolabs/project_template) repository. This command will run through the steps of cloning the project, updating all block submodules, and set the initial commit for your project. The new project folder will be made inside the current directory.

You will be prompted to enter values for `PK Host` and `PK Token`. These values will be put in your projects `nio.env` file. Pressing enter without typing in configuration values will not change the corresponding fields in `nio.env`.

An optional `--template` or `-t` can be specified to pull from a different project directory. This field will accept a repo name in the [niolabs GitHub](https;//github.com/niolabs) or an entire GitHub link.

Example:
```bash
nio new first_project
```
Will create a new folder in your current directory named `first_project` containing everything needed for your nio project.

Example (niolabs template):
```bash
nio new my_plant --template demo_plant
```

Will pull the demo_plant project from the official [niolabs GitHub](https;//github.com/niolabs) and place it in a directory named `my_plant`.

Example (GitHub template):
```bash
nio new my_project --template https://github.com/foo/bar
```

Will pull a nio project from the `bar` repository of a GitHub user `foo` and name it `my_project`.
