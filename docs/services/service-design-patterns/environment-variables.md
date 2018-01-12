# Environment Variables

The nio Platform allows you to define and use variables when configuring your instance, services, or blocks. These variables are called "environment variables" and are specified using the square bracket syntax: <br>`[[ ENV_VAR_NAME ]]`. There are several different use cases for environment variables which are detailed below.

---

## Access Tokens and Other Secrets

Often a block will need some sort of access token or password in its configuration. Rather than store those in the block config directly, where they are visible in plain text, we recommend using an environment variable for that. Add an entry to your environment variable file `nio.env`.
```
MY_SECRET: p@$$w0rd
```

Then, in your block config you can use that secret token by using the environment variable syntax: <br>`[[ MY_SECRET ]]`. The block will receive the proper value when the service is started, but the block's configuration will always contain the unreplaced environment variable.

---

## Different Environments

A large-scale nio system will generally run in multiple environments. Here are several examples:

1. A multi-tenant setup where the same project runs in many different locations. For example, a smart retail store system where the project runs in every store.
2. A staging environment used for validation and testing.
3. A local test environment used for building blocks or writing service unit tests.

For any of these setups, the use of environment variables can help you. If you find that a value may differ from one environment to the next \(e.g., an IP address, a database password, whether a service should run or not\), then replace that value with an environment variable and create a different env file for the respective environment. For example, your production env file \(`prod.env`\) may look something like this:

```
DB_HOST: real-data-host.com
DB_PASS: a357v34bs434vb34
```

but your local testing environment file \(`test.env`\) may look like this:

```
DB_HOST: localhost
DB_PASS: password
```

In your blocks and services, you can use `[[ DB_HOST ]]` as the database host and be assured that when you are running nio locally you aren't talking to the production database.

See the [Deployment](/deployment) section for more information.

---

## Setting Environment Variables

nio environment variables are slightly different than operating system environment variables. nio environment variables can also be set by operating system environment variables. This can be useful when running nio using Docker, systemd, or some other process manager where you can pass environment variables to the process.

In general, environment variables can be sourced from two places.

1. The operating system environment variables.

   ```bash
   $ export DB_HOST=localhost
   $ niod
   ```

   ```bash
   $ docker run -e DB_HOST=localhost nio_binary_image
   ```

2. The `.env` files in your project directory. Assuming you have a `prod.env` file in your project directory, you can source from that using the `-e` flag of `niod`.

   ```bash
   $ niod -e prod.env
   ```

In the event that an environment variable is set both at the system level and the local `.env` file level, the system environment variable will take precedence.
