# New project

The `new` command creates a fresh project from the official [project template](https://github.com/niolabs/project_template) repository. This command will run through the steps of cloning the project, updating all block submodules, and set the initial commit for your project. The new project folder will be made inside the current directory.

You will be prompted to enter values for `Pubkeeper hostname` and `Pubkeeper token`. These values will be put in your project's `nio.conf` file under the `[user_defined]` section. Pressing enter without typing in configuration values will leave the values in the `nio.conf` unchanged.

Additionally, it will prompt you with the option to create and/or install an SSL certificate for your nio instance.  This allows you to configure your nio instance with an additional layer of security and enables the nio System Designer to connect via HTTPS.  For more information on SSL certificates and their application, follow this [link](https://www.globalsign.com/en/ssl-information-center/what-is-an-ssl-certificate/).

An optional `--template` or `-t` can be specified to pull from a different project directory. This field will accept a repo name in the [niolabs GitHub](https://github.com/niolabs) or an entire GitHub link.

---

## Example:

```bash
nio new first_project
```
creates a new folder in your current directory named `first_project` containing everything needed for your nio project.

---

## Example (niolabs template):

```bash
nio new my_plant --template demo_plant
```

pulls the **demo_plant** project from the official [niolabs GitHub](https://github.com/niolabs/plant_demo) and places it in a directory named `my_plant`.

---

## Example (GitHub template):

```bash
nio new my_project --template https://github.com/foo/bar
```

pulls a nio project from the `bar` repository of a GitHub user `foo` and names it `my_project`.

---

## New project creation

Once you've executed one of the comands above, follow the prompts to configure your project. You can always open of nio.conf later to modify any values, but the nio-cli takes care of it for you automatically.

>**[info] default values**
>
>* if a prompt defines a default value, you may hit `Enter` to accept it.

**Configure your local nio instance:**
- Enter instance hostname or IP \[default: localhost\]:
- Enter instance port \[number, below 1024 requires "sudo", default: 8181\]:

**Configure Pubkeeper for instance communications:**
- Are you running a standalone Pubkeeper Server? \[y/N, default = N\]:
  - If "no" (the default):
    - Enter Pubkeeper hostname \[required\]:
    - Enter Pubkeeper token \[required\]:
  - If "yes":
    - Enter a complex, random string Pubkeeper will use to secure intra-instance communication \[required\]:

**Configure instance encryption:**
- Secure instance with SSL? \[y/N, default = N\]:
  - Generate a self-signed certificate/key \[y/N, default = N\]:
    - If "yes":
      - Enter two-letter country code:
      - Enter state:
      - Enter city:
      - Enter company/owner:
      - Enter user:
    - If "no":
      - Enter SSL certificate file location \[required\]:
      - Enter SSL private key file location \[required\]:

>**Once your project is created, the nio-cli will provide additional instructions on how to:**
>
>- Start your instance
>- Accept your self-signed cert (if applicable)
>- Add your instance to the nio System Designer



