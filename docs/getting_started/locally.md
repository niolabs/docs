# Running n.io Locally

The cloud is an easy way to get n.io up and running but doesn't fully encapsulate the distributed power of the n.io platform. To do that, we should run n.io on a local or edge node.

## Requirements

 * Python 3.4.5 or 3.5.2
 * A n.io binary python wheel

Running the n.io platform requires either python version `3.4.5` or `3.5.2`. Other versions of python 3.4 may work, but python 3.5.3 and above do not work. If you see `Bad magic number` errors when running a n.io binary, it is likely caused by an incompatible version of python.

You will need a python `.whl` file to install the n.io binary. This should have been provided to you as part of your license agreement. Reach out to n.io support if you need a new wheel file.

## Installation

Simply install the n.io wheel file using `pip`, probably like so:
```
pip3 install your_wheel_file.whl
```

After installation, you should be able to run `nio_run`. If that command is not available, make sure your python binary installation directory is on your PATH.

Some tasks are made easier by using the n.io CLI. This can be installed from pip as well:
```
pip3 install nio-cli
```

## First Project

Now that we have the n.io binary to run, we need a n.io project to run it against. You can obtain a n.io project template by cloning down the [Project Template repository](https://github.com/nioinnovation/project_template) or by using the n.io CLI. 

To use the CLI, run `nio new first_project`. This will create a directory called `first_project` in your working directory containing a n.io project.

To use git to set up the project, you will need to clone the template and then initialize the submodules which contain the blocks:
```
git clone https://github.com/nioinnovation/project_template.git first_project
cd first_project
git submodule update --init --recursive
```

Once the project directory is set up, we can run n.io from inside of it. Go to the project directory (`cd first_project`) and then run `nio_run`. You should see some log messages displayed but no errors. Logs should look something like this:
```
[2016-03-04 23:49:41.035] NIO [INFO] [main.WebServer] Server configured on 0.0.0.0 : 8181
[2016-03-04 23:49:41.035] NIO [INFO] [main.WebServer] Server configured on 0.0.0.0:8181
[2016-03-04 23:49:41.042] NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from:  to: created
[2016-03-04 23:49:41.055] NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from: created to: configuring
[2016-03-04 23:49:41.109] NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from: configuring to: configured
[2016-03-04 23:49:41.123] NIO [INFO] [main.WebServer] Starting server on 0.0.0.0:8181
[2016-03-04 23:49:41.226] NIO [INFO] [main.WebServer] Server 0.0.0.0:8181 started on 0.0.0.0:8181
[2016-03-04 23:49:41.226] NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from: configured to: starting
[2016-03-04 23:49:41.227] NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from: starting to: started
```

If you see those logs, it means n.io is up and running, congratulations!

## Add a local instance to the System Designer

Once we have a local instance running, we'll want to edit it using the System Designer. Log in to the System Designer and select a system to add your locally running n.io instance to. Once the system is selected, click the "Add New Instance" button at the top.

Give your instance a name, then specify `localhost` for host and `8181` for port. Leave the access mode as `basic` for now. You are telling the designer that your n.io instance is available at `http://localhost:8181` which is what our log messages from n.io indicated to us. You are also telling it to use basic authentication to communicate with the instance. 

Note this important detail about the System Designer: when you connect to a n.io instance to edit it you are communicating with that instance directly from your browser (via an XHR request). That means hostnames like `localhost` and other internal IP addresses work. It also means these instances won't be available to be designed through the System Designer unless you are able to access them from your machine.

You may see an issue regarding HTTPS and HTTP instances. Since you launched your instance and presumably didn't load any SSL certificates into it, the instance is accessible only by HTTP. However, if you are logged into the System Designer via HTTPS then an XHR request going over HTTP is not permitted (this is a browser restriction). Instead, log into the designer [via HTTP](http://designer.n.io). All of your instances and systems will be the same, only the n.io commands to edit these instances won't happen over HTTPS.

Once your instance is loaded and available, you can add services and blocks to it just like a cloud instance. Any errors or activity that happens will be available through the logs in your terminal that is running n.io. This makes local instances a much more useful tool for designing n.io systems where debugging is needed.

## Adding Blocks to a Project

Before we move on, you're going to want to add some blocks to your project. Press ctrl-c to ext n.io. We'll add four popular blocks using the n.io CLI to get you started:

```
nio add logger simulator filter dynamic_fields
```

If you prefer to install the blocks without the CLI, clone the relevant block repositories into the `blocks/` folder of your project. In other words, from your project root you can run:
```
git submodule add https://github.com/nio-blocks/logger.git blocks/logger
```
