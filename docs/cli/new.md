# New project

The `new` command creates a fresh project from the official [project template](https://github.com/niolabs/project_template) repository. This command will run through the steps of cloning the project, updating all block submodules, and set the initial commit for your project. The new project folder will be made inside the current directory.

The `new` command accepts several options to allow for quick instance configuration. Your instance hostname and runtime port can be specified with `--ip` and `--port`. When these flags are set, nio will configure to run at `ip:port` rather than the default `127.0.0.1:8181`. The changes made from these flags are reflected in your project `nio.conf` file under the `[user_defined]` section.

Pubkeeper communication settings can be added using the `--pubkeeper-hostname` and `--pubkeeper-token` options. When these are set, your nio instance will configure to connect to a specified Pubkeeper server for system wide communication. The changes made from these flags are reflected in your project `nio.conf` file under the `[user_defined]` section.

Instance authentication can be configured by passing `--username` and `--password` options. This will update the authentication used by your instance for all HTTP requests. By default, instances use basic authentication credentials (Admin:Admin) to authorize access. The changes made from these flags are reflected in your project `etc/users.json` and `etc/permissions.json` files.

Additionally, a `--ssl` flag can be passed to create and/or install an SSL certificate for your nio instance.  This allows you to configure your nio instance with an additional layer of security and enables the nio System Designer to connect via HTTPS.  For more information on SSL certificates and their application, follow this [link](https://www.globalsign.com/en/ssl-information-center/what-is-an-ssl-certificate/).

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

## Example (configure Pubkeeper):

```bash
nio new my_project --pubkeeper-hostname <system_id>.pubkeeper.nio.works --pubkeeper-token <pubkeeper_token>
```

creates a new folder in your current directory named `my_project` with pubkeeper settings configured for system wide communication.

---

## Example (configure authentication):

```bash
nio new my_project --username <username> --password <password>
```

creates a new folder in your current directory named `my_project` with a specified user created to access this instance. Use your configured `<username>` and `<password>` values in the [System Designer](/system-designer/reference.md#connect-to-a-local-instance).

---

## Example (configure encryption):

```bash
nio new my_project --ssl
```

creates a new folder in your current directory named `my_project`. Follow the prompts to configure instance encryption enabling secure authentication for your new instance.

---

## New project creation

Once you've executed one of the commands above, follow the prompts to configure your project. You can always open of nio.conf later to modify any values, but the nio-cli takes care of it for you automatically.

>**[info] default values**
>
>* if a prompt defines a default value, you may hit `Enter` to accept it.

**Configure your local nio instance:**
- `nio new <project> --ip <ip> --port <port>`
- Instance hostname or IP \[default: 127.0.0.1\]:
- Instance port \[number, below 1024 requires superuser access, default: 8181\]:

**Configure Pubkeeper for instance communications:**
- `nio new <project> --pubkeeper-hostname <hostname> --pubkeeper-token <token>`

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



