# New project

The `new` command creates a fresh project from the official [project template](https://github.com/niolabs/project_template) repository. This command will run through the steps of cloning the project, updating all block submodules, and set the initial commit for your project. The new project folder will be made inside the current directory.

You will be prompted to enter values for `Pubkeeper hostname` and `Pubkeeper token`. These values will be put in your project's `nio.conf` file under the `[user_defined]` section. Pressing enter without typing in configuration values will leave the values in the `nio.conf` unchanged.

Additionally, it will prompt you with the option to create and/or install an SSL certificate for your nio instance.  This allows you to configure your nio instance with an additional layer of security and enables the nio System Designer to connect via HTTPS.  For more information on SSL certificates and their application, follow this [link](https://www.globalsign.com/en/ssl-information-center/what-is-an-ssl-certificate/).

An optional `--template` or `-t` can be specified to pull from a different project directory. This field will accept a repo name in the [niolabs GitHub](https://github.com/niolabs) or an entire GitHub link.

Example:
```bash
nio new first_project
```
creates a new folder in your current directory named `first_project` containing everything needed for your nio project.

Example (niolabs template):
```bash
nio new my_plant --template demo_plant
```

pulls the **demo_plant** project from the official [niolabs GitHub](https://github.com/niolabs/plant_demo) and places it in a directory named `my_plant`.

Example (GitHub template):
```bash
nio new my_project --template https://github.com/foo/bar
```

pulls a nio project from the `bar` repository of a GitHub user `foo` and names it `my_project`.
