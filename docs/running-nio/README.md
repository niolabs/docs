# Running nio locally

>**[info] Prerequisites**
>
>* **The nio Platform installed on your device**: follow the [installation instructions](/installation/nio)


The command to run nio locally is `niod`. This will start running a nio instance on your machine. Run this command from the root of a project directory.

---
## Create a project
<img class="right shadow" src="/img/cloud/addInstanceButton.png" width="200" />
The easiest way to create and run a new nio project is to first create a new local instance in the System Designer and then copy and run the `nio new` command containing your system's Pubkeeper credentials.

<img class="right border" src="/img/addLocalInstance.png" width="250" />
1. Open the **nio System Designer** in a browser: http://app.n.io/design (note the http protocol for local instances without SSL certificates).
1. Select your system card from the grid.
1. Click **add instance** on the left side of your screen.
  * Check the **local instance** checkbox.
  * In the **instance name** box, enter an instance name.
1. The rest of the text inputs will be pre-filled with default values that you may edit if necessary.
1. At the bottom, copy the nio-cli command that will create your project with the correct Pubkeeper credentials.
<br>
<br>

Back in your terminal, paste the command copied from the create instance modal into the command line to create your project.
```
nio new LocalInstance --pubkeeper-hostname xxxxx.pubkeeper.nio.works --pubkeeper-token xxxxxxxx
```

> Note: you need nio-cli 0.6.0+ to run this command. Type `nio --version` to see which version of the nio-cli you are running. You can update with `pip3 install -U nio` or `pip install -U nio` (depending which pip you have in your environment).

When it prompts you for an optional secure instance configuration, choose Yes (Y). Press return for the default on all following prompts.

Navigate into your new project directory
```
cd LocalInstance
```
and run nio:
```
niod
```
Log messages should display in your terminal, similar to the following output. There should be no errors.

```
NIO [INFO] [main.WebServer] Server configured on 0.0.0.0:8181
NIO [INFO] Component: ServiceManager status changed to: created
NIO [INFO] Component: ServiceManager status changed from: created to: configuring
NIO [INFO] Component: ServiceManager status changed from: configuring to: configured
NIO [INFO] [main.WebServer] Starting server on 0.0.0.0:8181
NIO [INFO] [main.WebServer] Server 0.0.0.0:8181 started on 0.0.0.0:8181
NIO [INFO] Component: ServiceManager status changed from: configured to: starting
NIO [INFO] Component: ServiceManager status changed from: starting to: started
```

If you see those logs, nio is up and running. Congratulations!

>By default, new projects use port 8181. If port 8181 isn’t available, you'll see an error. The value of NIOPORT in your project's `nio.conf` file under the `[user_defined]` section and the port for your local instance in the System Designer should match.

Once your instance is loaded and available, you can add services and blocks in the same manner as a [cloud instance](https://workshops.n.io/system-designer/).

Available nio Blocks can be explored in the nio [Block Library](https://blocks.n.io) where you will find a summary of the block's purpose, a list of its properties, commands, inputs, and outputs, and a link to the block code repository.

---
## Add an existing local instance/project to the <span class="allow-caps">System Designer</span>

<img class="right shadow" src="/img/cloud/addInstanceButton.png" width="200" />
You can also add an existing local instance to the **System Designer**. Make sure your local instance is running.

1. Open the **nio System Designer** in a browser: http://app.n.io/design.
<img class="right border" src="/img/addLocalInstance.png" width="250" />
1. Select your system card from the grid.
1. Click **add instance** on the left side of your screen.
  * Check the **local instance** checkbox.
  * In the **instance name** box, enter an instance name.
1. The rest of the text inputs will be pre-filled with default values that you may edit if necessary.
1. Click **accept**.


When the System Designer connects to a nio instance, it communicates with that instance directly from your browser via an XHR request. Hostnames like `localhost` and other internal IP addresses will work. **You must have access to the localhost or other IP address from your machine to use the System Designer.**

---
## http
#### {#http}

You may see an issue regarding HTTPS and HTTP instances.


> **[info] security error?**
>
> If you launched your instance without any SSL certificates, the instance is only accessible via HTTP. If you are logged into the System Designer via HTTPS, your browser will restrict any XHR requests going over HTTP.
>
> To connect to a local HTTP instance of nio with the System Designer, you'll need to log into the designer via HTTP at [http://app.n.io/design](http://app.n.io/design). All of your instances and systems will be the same, the only difference is, the nio commands to edit these instances won't happen over HTTPS.

---
## Run nio from outside the project directory

`niod` can be run from outside of a project directory by using the `-r` flag and specifying the location of the project directory. For example:

```
niod -r path/to/my_project
```

---
## Run in the background

You can run a project in the background on MacOS and Linux using `nohup` (so you can close your terminal):
```
nohup niod -r path/to/my_project 2>&1 > /dev/null &
```

---
## View your logs

When running in background mode, you can monitor your logs using the “tail” command:
```
tail -f /path/to/my_project/logs/main.log
```

---
## Stop your project

```
nio shutdown -p {NIOPORT}
```
> NIOPORT is set in your project's nio.conf file under the [user_defined] section

---
## `nio.env` is obsolete

nio Binaries released after January 26, 2018, no longer use the `nio.env` file for user-defined variables. Instead, all of these variables are located under the `[user_defined]` section of `nio.conf`.

>If you would like to use your old projects with the latest binary, run this [script](https://gist.github.com/tlugger/2da9c8e615265243c07c76549f402ca6) from your project directory with `python move-conf.py` to easily move your variables from `nio.env` to `nio.conf`.
