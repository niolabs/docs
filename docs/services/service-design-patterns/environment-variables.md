# Environment variables

The nio Platform allows you to define and use variables when configuring your instance, services, or blocks. These variables are called "environment variables" and are referenced using the square bracket syntax: `[[ ENV_VAR_NAME ]]`. There are several different use cases for environment variables which are detailed below.

---

## Access tokens and other secrets

Often a block will need some sort of access token or password in its configuration. Rather than store those in the block config directly, where they are visible in plain text, we recommend using an environment variable for that. There are two ways to manage your environment variables.  The easiest way is to use the [Instance Editor](/system-designer/designer-tasks.md#instance-sd).  If you are running an instance locally, you can add an entry to your configuration file `nio.conf` under the `[user_defined]` section at the top of the file.
```
MY_SECRET=p@$$w0rd
```

Then, in your block config you can use that secret token by using the environment variable syntax: `[[ MY_SECRET ]]`. The block will receive the proper value when the service is started, but the block's configuration will always contain the unreplaced environment variable.

---

## Different environments

A large-scale nio system will generally run in multiple environments. Here are several examples:

1. A multi-tenant setup where the same project runs in many different locations. For example, a smart retail store system where the project runs in every store.
1. A staging environment used for validation and testing.
1. A local test environment used for building blocks or writing service unit tests.

For any of these setups, the use of environment variables can help you. If you find that a value may differ from one environment to the next \(e.g., an IP address, a database password, whether a service should run or not\), then replace that value with an environment variable and create a different `.conf` file for the respective environment. For example, your production `.conf` file \(`prod.conf`\) may look something like this:

```
DB_HOST=real-data-host.com
DB_PASS=a357v34bs434vb34
```

but your local testing environment file \(`test.conf`\) may look like this:

```
DB_HOST=localhost
DB_PASS=password
```
### Chaining `.conf` files  

One can have multiple configuration files, each with a `[user_defined]` section, and chain them together using the `-s` flag. Each subsequent file definitions will override former definitions when the same variable is specified, for example:


   ```bash
   $ niod -s prod.conf -s redis-prod.conf
   ```

This will take your production environment and then implement the more specific configuration for your Redis database found in `redis-prod.conf`.

In your blocks and services, you can use `[[ DB_HOST ]]` as the database host and be assured that when you are running nio locally you aren't talking to the production database.

See the [Deployment](/deployment/README.md) section for more information.

---

## Setting environment variables

The nio Platform allows the definition of an environment variable in three distinct ways. The following also describes the priority order from highest to lowest.
  1. The variable is defined as an OS environment variable.
  2. The variable is saved using persistence, and either edited manually (local persistence) or through a user interface (remote persistence).
  3. The variable is defined as an entry under `[user_defined]` in a nio configuration file.

Setting a nio environment variable as an operating system environment variable can be useful when running nio using Docker, systemd, or some other process manager where you can pass environment variables to the process.

Some examples of environment variable definitions are illustrated below.

1. Defining environment variables from the operating system level:

   ```bash
   $ export DB_HOST=localhost
   $ niod
   ```

   ```bash
   $ docker run -e DB_HOST=localhost nio_binary_image
   ```

2. Defining environment variables using `.conf` files in your project directory under a `[user_defined]` section:

  Assuming you have a `prod.conf` file in your project directory, you can specify it using using the `-s` flag of `niod`.

   ```bash
   $ niod -s prod.conf
   ```

Again, in the event that an environment variable is set both at the system level and the local `.conf` file level, the system environment variable will take precedence.