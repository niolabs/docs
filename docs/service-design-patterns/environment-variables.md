# Environment Variables

n.io allows you to define and use variables when configuring your instance, services, or blocks. These variables are called "environment variables" and are specified using the square bracket syntax like so: `[[ ENV_VAR_NAME ]]`. There are several different use cases for environment variables which are detailed below.

## Access Tokens and Other Secrets

Often times a block will need some sort of access token or password in its configuration. Rather than store those in the block config directly, where they are visible in plaintext, we recommend using an environment variable for that. To do so, add an entry to your `nio.env` (or whatever env file you are using) like so:
```
MY_SECRET: p@$$w0rd
```

Then, in your block config you can use that secret token by using the environment variable syntax like so: `[[ MY_SECRET ]]`. The block will receive the proper value when the service is started but the block's configuration will always contain the unreplaced environment variable value.

## Different Environments

A large-scale n.io system will generally have different environments that it is run in. There are several examples of this:

1. A multi-tenant setup where the same project runs in many different locations. For example, a smart retail store system where the project runs in every store.
2. A staging environment used for validation and testing.
3. A local test environment used for building blocks or writing service unit tests.

For any of these setups, the use of environment variables can help you. If you find that a value may differ from one environment to the next (e.g., an IP address, a database password, whether a service should run or not) then replace that value with an environment variable and create a different env file for the respective environment. For example, your production env file (`prod.env`) may look something like this:
```
DB_HOST: real-data-host.com
DB_PASS: a357v34bs434vb34
```

but your local testing environment file (`test.env`) may look like this:
```
DB_HOST: localhost
DB_PASS: password
```
Now in your blocks and services, you can use `[[ DB_HOST ]]` as the database host and be assured that when you are running n.io locally you aren't talking to the production database.

More of this information is detailed in the [Deployment](/deployment) section of these docs.

## Setting Environment Variables

n.io environment variables are slightly different than OS system environment variables. However, to make that even more confusing, n.io environment variables can be set by OS system environment variables. This is often useful when running n.io using Docker, systemd, or some other process manager where you can pass environment variables to the process.

In general, environment variables can be sourced from two places:

1. The OS system environment variables
Examples:
```bash
$ export DB_HOST=localhost
$ nio_run
```
```bash
$ docker run -e DB_HOST=localhost nio_binary_image
```
2. The `.env` files in your project directory. Assuming you have a `prod.env` file in your project directory, you can source from that using the `-e` flag of `nio_run` like so:
```bash
$ nio_run -e prod.env
```

In the event that an environment variable is set both at the system level and also in the `.env` file, the system environment variable will take precedence and be used.
