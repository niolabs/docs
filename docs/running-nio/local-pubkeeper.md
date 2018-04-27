# Running a Local Pubkeeper Server

Sometimes you don't want to have to connect to the managed Pubkeeper server in the cloud but rather run and connect to one on your local network. This allows for the design of fully offline systems that do not require an internet connection.

---

## Installation

If your nio license supports it, you may download a Pubkeeper Server Python wheel from your [binary download page](https://account.n.io/binaries/download). This wheel contains the necessary libraries to run the Pubkeeper server.

Install it like any other wheel, with pip:

```
pip install pubkeeper.server.core-1.1.3-py3-none-any.whl
```

This will make the `pubkeeper.server.core` library available in your Python environment. Contact support if your installation fails.

---

## Running the Server Standalone

The installation of the server library also installs an executable that you can use to run the Pubkeeper server as a standalone process. Create a file called `pubkeeper.conf` with the following contents:
```
[pubkeeper_server]
port = 9898

[auth]
provider = pubkeeper.server.core.auth.internal.InternalAuthProvider
token = your_secret_token
```

In the same directory as that file, start the Pubkeeper server:
```
pk_server
```

This will launch a Pubkeeper server on port 9898 using the [Internal Auth Module](https://docs.pubkeeper.com/python-server/auth/internal.html) that will only accept clients using the token specified in the conf file. More details about running the Pubkeeper server in a standalone mode can be found on [the Pubkeeper documentation pages](https://docs.pubkeeper.com/python-server/).

---

## Running the Server in the nio Instance

nio binaries also come with the ability to run the Pubkeeper server in the nio core process. This still requires that you install the Pubkeeper server library in the installation steps above. Simply having the nio binary does not mean that you have the Pubkeeper server installed.

>**[info] Systems**
>
> Remember, each nio system should have one and only one Pubkeeper server running. So you don't want to run the Pubkeeper in every one of your instances in a system. Instead, choose one instance to run the Pubkeeper server, likely the most highly available instance.
>

To enable the Pubkeeper server to run in your nio instance, alter your nio project configuration file (e.g., `nio.conf`) to have a `[pubkeeper_server]` section with the setting of `standalone` set to `True`. Example:
```
[pubkeeper_server]
standalone = True
```

This configuration section is where you can configure other Pubkeeper server settings for the embedded server too.

A helpful trick to do this is to make use of the nio executable's ability to chain configuration files together. In your project you will see a `pk_server.conf` file with some partial configuration that applies to the Pubkeeper server. To include this configuration in your nio instance, simply include it when you run nio with the `-s` flag.
```
niod -s nio.conf -s pk_server.conf
```

You still need to specify `nio.conf` in the example above, otherwise nio would try to only load the `pk_server.conf` configuration file which only contains partial configuration.
