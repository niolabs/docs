# Running nio Locally

The cloud is an easy way to get nio up and running, but it doesn't fully capture the distributed power of the nio Platform. To see the power of nio as a distributed system, you should install and run nio on a local or edge node. In this guide, you will create a local instance that uses a cloud-based [Pubkeeper](/Pubkeeper) server to handle communications.

Running the nio Platform requires Python version 3.4 or greater.

Requirements

* Download Python 3.4 or greater from [https://www.python.org/downloads/](https://www.python.org/downloads/).
* Obtain the nio binary Python wheel file (`.whl`) with your license agreement.

## Download nio

Once you have signed up for a license, download nio from the following URL:

https://app.n.io/binaries/download

## Install the nio binary and CLI

To install nio on your computer, enter the following command:
```
pip3 install your_wheel_file.whl
```

To install the nio Command Line Interface \(CLI\), enter the following command:
```
pip3 install nio-cli
```

### To Upgrade the nio binary and CLI

If you already have a version of nio installed and want to upgrade it, enter the following command:
```
pip3 install -U your_wheel_file.whl
```

To upgrade the nio Command Line Interface \(CLI\), enter the following command:
```
pip3 install -U nio-cli
```

## Create a Project

Now that the nio binary is installed, you need a nio project to run it against. A project folder is a way to organize and maintain the blocks, variables, and configurations that you want use with an instance of nio. The easiest way to create a new nio project is by using the nio CLI. If you prefer not to use the nio CLI, you can create a project by cloning the [Project Template repository](https://github.com/niolabs/project_template). Follow the instructions below for your preferred method.

### Create a new nio Project Using the nio CLI
To create a project template using the CLI, enter the following command:

`nio new first_project`

This will create a `first_project` directory in your working directory that contains your nio project.

### Download a nio Project Template Using Git
To download the project template using Git, clone the template and initialize the submodules, which contain the blocks, using the following commands:
```
git clone https://github.com/niolabs/project_template.git first_project
cd first_project
git submodule update --init --recursive
```

## Set up the Environment

You will want to use the System Designer to see your local instance running.

Open the **System Designer** in a browser.

  https://designer.n.io/

If you don't already have a system you want to use for this project in the designer, click the **`+`** button to create one.

When you complete the **create new system** window and click **accept**, a new Pubkeeper server will be created in the cloud to handle the communications in your system.

To connect your local nio project to the Pubkeeper server, you will need to configure your project.

### Configure Your Local Project to use the Cloud Pubkeeper Server

With your system selected, click **edit** in the contextual toolbar to open the system's configuration.

{% include "/includes/pubkeeper-config.md" %}

### Run nio

With your project installed and Pubkeeper communication configured, you are ready to run your nio binary. In your terminal, from the root of your project directory, enter the following command:
```
nio_run
```
> If that command is not available, make sure your Python binary installation directory is on your PATH.

> If you need help setting your PATH in Windows, click [here](https://msdn.microsoft.com/en-us/library/aa922003.aspx).

> If you need help setting your PATH in MacOS, click [here](http://osxdaily.com/2014/08/14/add-new-path-to-path-command-line/).

Log messages should display, similar to the following output, but there should be no errors.

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

If you see those logs, nio is up and running. Congratulations!

## Add a Local Instance

Once you have a local instance running, you can edit it using the System Designer. The log messages indicate that your nio instance is available at `http://localhost:8181` and you need basic authentication to communicate with the instance. To connect to your local instance

1. Select the name of your system, either in the left navigation panel or the breadcrumb above the contextual toolbar.
1. Click **create local instance**.
1. Complete the **create local instance** window:
  * In the **instance name** box, enter your instance name.
  * In the **hostname** box, enter **localhost**.
  * In the **port** box, enter **8181**.
  * Leave the **access mode** as **basic**.
1. Click **accept**.
1. Wait for the instance to spin-up and note the name of the new instance on the left.

> Note: When the System Designer connects to a nio instance, it communicates with that instance directly from your browser via an XHR request. Hostnames like `localhost` and other internal IP addresses will work. You must have access to the localhost or other IP address from your machine to use the System Designer.

You may see an issue regarding HTTPS and HTTP instances. Since you launched your instance and presumably didn't load any SSL certificates, the instance is accessible only by HTTP. However, if you are logged into the System Designer via HTTPS, your browser will restrict an XHR request going over HTTP. To connect to a local instance, you can log into the designer via HTTP at http://designer.n.io. All of your instances and systems will be the same, except the nio commands to edit these instances won't happen over HTTPS.

Once your instance is loaded and available, you can add services and blocks in the same manner as the [cloud instance](/getting_started/in_the_cloud#create-a-service).

Available blocks can be explored in the [Block Library](blocks.n.io) where you will find a summary of the block's purpose, a list of its properties, commands, inputs, and outputs, and a link to the block code repository.

## Create a Service

1. Select the name of your instance under the system name in the left navigation panel or in the breadcrumb above the contextual toolbar.
1. Click **create new service**.
1. Complete the **create new service** window:
  1. In the **service name** box, enter a service name.
  1. Leave the **service type** as **Service**.
1. Click **accept**.
1. Click **save** in the toolbar.
1. Click **auto-start off** in the toolbar.

## Add Blocks
Once you have successfully created a service, you will be switched to the service context where blocks are available in the Block library for you to build your logic. Blocks can either be added in the System Designer or from the command line.

### To Add a Block in the System Designer
1. In the **Block library** search box, enter a search term. As you type, the list is filtered.
* If the block is not displayed, click **available**, **installed**, and **configured** to search for the block.
* If the block is not already pre-installed, click the **install block** button which resembles a cloud with a down arrow.
1. Drag the block type to the canvas.
1. Name the block.
1. Click **accept**.

### To Add Blocks Manually

1. From the project root directory, add the relevant block repository into the `blocks/` folder as a submodule. For example, the logger block:
```
git submodule add https://github.com/nio-blocks/logger.git blocks/logger
```
This can also be done with the nio CLI with `nio add logger`.

Learn more about how to configure your blocks and link them together to perform various services in the tutorials at https://workshops.n.io/.
