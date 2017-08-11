# Running {{ book.product}} Locally

The cloud is an easy way to get {{ book.product}} up and running, but doesn't fully encapsulate the distributed power of the {{ book.product}} platform. Instead, you should run {{ book.product}} on a local or edge node.

Running the {{ book.product}} platform requires Python version 3.4.5 or 3.5.2. Other versions of Python 3.4.x may work, but Python 3.5.3 and later do not work. When running the {{ book.product}} binary, the `Bad magic number` error is most likely caused by an incompatible version of Python.

Requirements

* Download Python 3.4.5 or 3.5.2 from [https://www.python.org/downloads/](https://www.python.org/downloads/).
* Obtain the {{ book.product}} binary Python wheel file (`.whl`) with your license agreement.

## Install

To install {{ book.product}}, enter the following command:
```
pip3 install your_wheel_file.whl
```
To run {{ book.product}}, enter the following command:

`nio_run`

If that command is not available, make sure your Python binary installation directory is on your PATH.

To install the {{ book.product}} Command Line Interface \(CLI\), enter the following command:
```
pip3 install nio-cli
```

## Create Project

Now that we have the {{ book.product}} binary to run, we need a {{ book.product}} project to run it against. Obtain a {{ book.product}} project template by cloning the [Project Template repository](https://github.com/nioinnovation/project_template) or  use the {{ book.product}} CLI.

To clone the project template using CLI, enter the following command:

`nio new first_project`

The `first_project` directory is created in your working directory containing the {{ book.product}} project.

To clone the project template using git, clone the template,  and initialize the submodules which contain the blocks.
```
git clone https://github.com/nioinnovation/project_template.git first_project
cd first_project
git submodule update --init --recursive
```
To run {{ book.product}}, enter the following commands:
```
cd first_project
nio_run
```
The log messages display, similar to the following output, but there should be no errors.

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

If you see those logs, {{ book.product}} is up and running. Congratulations!

## Add a Local Instance

Once you have a local instance running, you can edit it using the System Designer. Based on the log messages, your {{ book.product}} instance is available at `http://localhost:8181` and you need basic authentication to communicate with the instance.

To create a local instance:

1. Log in to the System Designer.
2. Click the **+** button in the lower-left corner to create and name a new system.
3. Click **Accept**.
4. Select the name of the system.
5. Click **Add new instance**. 
6. Type the name of the instance, enter **localhost** for host and **8181** for port, and leave the access mode as **basic**.
7. Click **Accept**.
8. Wait for the instance to spin-up and note the name of the new instance on the left.

Note: When you connect to a {{ book.product}} instance, you are communicating with that instance directly from your browser via an XHR request. Hostnames like `localhost` and other internal IP addresses will work. You must have access to the localhost or other IP address from your machine to use the System Designer. 

You may see an issue regarding HTTPS and HTTP instances. Since you launched your instance and presumably didn't load any SSL certificates, the instance is accessible only by HTTP. However, if you are logged into the System Designer via HTTPS, then an XHR request going over HTTP is not permitted due to a browser restriction. Instead, log into the designer via HTTP. All of your instances and systems will be the same, except the {{ book.product}} commands to edit these instances won't happen over HTTPS.

Once your instance is loaded and available, you can add services and blocks in the same manner as the cloud instance. Any errors or activity are available in the logs in your terminal that is running {{ book.product}}. When you need to debug a system, a local instance is a useful tool.

## Add Blocks to a Project

Before we move on, you're going to want to add some blocks to your project. Blocks can be added in the System Designer or from the command line.

nio blocks are installed to instances using the Block Library. The collection of blocks created by {{ book.product }} is also stored in the [nio-blocks GitHub repository](https://github.com/nio-blocks). You can search for blocks in the System Designer or in GitHub. 

To add a block in the System Designer:

1. Click the **Block Library** in the upper-right corner.
2. In the Search box, enter the name of a block. As you type, the list is filtered.
3. Click the **Install Block** button which resembles a cloud with a down arrow.
4. Drag a block onto the canvas.
5. Type the name of the block and click **Accept**. 

To add private blocks manually:

1. From your private site, determine the URL of the block you want to add.
2. From the project root directory, clone the relevant block from your private repository into the `blocks/` folder
```
git submodule add https://github.com/yourprivate-blocks/logger.git blocks/logger
```
3. Restart the System Designer.
4. Click the **Block Library** in the upper-right corner.
5. In the Search box, enter the name of a block. As you type, the list is filtered.
6. Drag the your block onto the canvas.
7. Type the name of the block and click **Accept**. 