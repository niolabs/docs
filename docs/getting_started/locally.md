# Running n.io Locally

The cloud is an easy way to get n.io up and running, but doesn't fully encapsulate the distributed power of the n.io platform. To do that, we should n.io on a local or edge node.

Running the n.io platform requires either Python version `3.4.5` or `3.5.2`. Other versions of Python 3.4 may work, but Python 3.5.3 and later do not work. When running the n.io binary, the `Bad magic number` error is most likely caused by an incompatible version of Python.

Requirements

* Python 3.4.5 or 3.5.2
* A n.io binary Python wheel

* Download Python from [https://www.python.org/downloads/](https://www.python.org/downloads/).

* Obtain the Python `.whl` file from n.io with your license agreement.

See support if you require a new wheel file.

## Installation

To install n.io:

Type the following command:

```
pip3 install your_wheel_file.whl
```

To run n.io:

Type the following command:

`nio_run`

If that command is not available, make sure your Python binary installation directory is on your PATH.

To install CLI \(Command Line Interface\):

Type the following command:

```
pip3 install nio-cli
```

## First Project

Now that we have the n.io binary to run, we need a n.io project to run it against. You can obtain a n.io project template by cloning down the [Project Template repository](https://github.com/nioinnovation/project_template) or by using the n.io CLI.

To clone the project template using CLI:

1. Run `nio new first_project`. 
2. The `first_project` directory is created in your working directory containing the n.io project.

To clone the project template using git:

Clone the template and then initialize the submodules which contain the blocks by entering the following commands:

```
git clone https://github.com/nioinnovation/project_template.git first_project
cd first_project
git submodule update --init --recursive
```

To run n.io:

1. Enter `cd first_project` to go to the project directory.
2. Type `nio_run`.

Log messages will be displayed, but there should be no errors.

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

Once we have a local instance running, we'll want to edit it using the System Designer. Based on the log messages, your n.io instance is available at `http://localhost:8181` and you need to tell it to use basic authentication to communicate with the instance. 



To create a local instance:

1. Log in to the System Designer.
2. Click the "+" icon on the lower left corner to create and name a new system.
3. Click "Accept."
4. Select the name of the system you created.
5. Click "Add New Instance."
6. Type the name of the instance, enter  `localhost` for host and `8181` for port, and leave the access mode as
   `basic.`

7. Click "Accept".
8. Wait for the instance to spin-up and note the name of the new instance on the left side of the screen.



Give your instance a name, then specify `localhost` for host and `8181` for port. Leave the access mode as `basic` for now. You are telling the designer that your n.io instance is available at `http://localhost:8181` which is what our log messages from n.io indicated to us. You are also telling it to use basic authentication to communicate with the instance.

Note this important detail about the System Designer: when you connect to a n.io instance to edit it you are communicating with that instance directly from your browser \(via an XHR request\). That means hostnames like `localhost` and other internal IP addresses work. It also means these instances won't be available to be designed through the System Designer unless you are able to access them from your machine.

You may see an issue regarding HTTPS and HTTP instances. Since you launched your instance and presumably didn't load any SSL certificates into it, the instance is accessible only by HTTP. However, if you are logged into the System Designer via HTTPS then an XHR request going over HTTP is not permitted \(this is a browser restriction\). Instead, log into the designer [via HTTP](http://designer.n.io). All of your instances and systems will be the same, only the n.io commands to edit these instances won't happen over HTTPS.

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

//////

[http://python.org/downloads](http://python.org/downloads)

