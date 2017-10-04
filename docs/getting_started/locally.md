# Running {{ book.product}} Locally

The cloud is an easy way to get {{ book.product}} up and running, but doesn't fully encapsulate the distributed power of the {{ book.product}} platform. Instead, you should run {{ book.product}} on a local or edge node.  In this guide, you will create a local instance that uses a cloud-based Pubkeeper server to handle communications.

Running the {{ book.product}} platform requires Python version 3.4 or greater.

Requirements

* Download Python 3.4 or greater from [https://www.python.org/downloads/](https://www.python.org/downloads/).
* Obtain the {{ book.product}} binary Python wheel file (`.whl`) with your license agreement.

## Download {{ book.product}}

Download {{ book.product}} from the following URL:

https://app.n.io/binaries/download

## Install the {{ book.product}} binary and CLI

To install {{ book.product}}, enter the following command:
```
pip3 install your_wheel_file.whl
```

To install the {{ book.product}} Command Line Interface \(CLI\), enter the following command:
```
pip3 install nio-cli
```

## Upgrade the {{ book.product}} binary and CLI

To upgrade {{ book.product}}, enter the following command:
```
pip3 install -u your_wheel_file.whl
```

To upgrade the {{ book.product}} Command Line Interface \(CLI\), enter the following command:
```
pip3 install -u nio-cli
```

## Create a Project

Now that you have the {{ book.product}} binary to run, you need a {{ book.product}} project to run it against. Obtain a {{ book.product}} project template by cloning the [Project Template repository](https://github.com/niolabs/project_template) or use the {{ book.product}} CLI.


### Download using the {{book.product}} CLI
To clone the project template using CLI, enter the following command:

`nio new first_project`

The `first_project` directory is created in your working directory containing the {{ book.product}} project.

### Download using git
To clone the project template using git, clone the template, and initialize the submodules which contain the blocks.
```
git clone https://github.com/niolabs/project_template.git first_project
cd first_project
git submodule update --init --recursive
```

## Set up {{book.product}} environment

After adding the new project, change to the project directory
```
cd first_project
```
## Create a System

1. Open the **System Designer** in a browser.

  https://designer.n.io/

1. In the lower-left corner, click the **`+`** button to build.
1. Complete the **Create a new system** window:
  1. In the **System name** box, enter your system name.
  1. Select **Auto** for the Pubkeeper configuration. This is the default.
1. Click **Accept**.
1. Click **Edit** in the contextual toolbar to open the system's configuration.
> Make note of the values for **host** and **token** which will be used in the following steps.
1. From your terminal, in your first_project directory, open the `nio.env` file.
1. Update the following four lines in the `# Pubkeeper Client` section
```
PK_TOKEN: [your copied token]
PK_HOST: [your copied host]
PK_PORT: 443
PK_SECURE: True
```
1. Update the following three lines in the `# Websocket Brew Variables` section
```
WS_HOST: [your copied host, replacing `pubkeeper` with `websocket`]
WS_PORT: 443
WS_SECURE: True
```

1. To run {{ book.product}}, enter the following command:
```
nio_run
```
> If that command is not available, make sure your Python binary installation directory is on your PATH.

  * If you need help setting your PATH in Windows, click [here](https://msdn.microsoft.com/en-us/library/aa922003.aspx).
  * If you need help setting your PATH in MacOS, click [here](http://osxdaily.com/2014/08/14/add-new-path-to-path-command-line/).

1. The log messages display, similar to the following output, but there should be no errors.

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

1. Select the name of your system in the left navigation panel or on the breadcrumb above the contextual toolbar.

  ![](/img/hierarchy.gif)

1. Click **Add new instance**.
1. Complete the **Create a new cloud instance** window:
  1. In the **Instance name** box, enter your instance name.
  1. In the **Host name** box, enter **localhost**.
  1. In the **Port** box, enter **8181**.
  1. Leave the **Access mode** as **basic**.
1. Click **Accept**.
1. Wait for the instance to spin-up and note the name of the new instance on the left.

Note: When you connect to a {{ book.product}} instance, you are communicating with that instance directly from your browser via an XHR request. Hostnames like `localhost` and other internal IP addresses will work. You must have access to the localhost or other IP address from your machine to use the System Designer.

You may see an issue regarding HTTPS and HTTP instances. Since you launched your instance and presumably didn't load any SSL certificates, the instance is accessible only by HTTP. However, if you are logged into the System Designer via HTTPS, then an XHR request going over HTTP is not permitted due to a browser restriction. Instead, log into the designer via HTTP. All of your instances and systems will be the same, except the {{ book.product}} commands to edit these instances won't happen over HTTPS.

Once your instance is loaded and available, you can add services and blocks in the same manner as the cloud instance. Any errors or activity are available in the logs in your terminal that is running {{ book.product}}. When you need to debug a system, a local instance is a useful tool.

## Create a Service

1. Select the name of your instance under the system name in the left navigation panel or on the breadcrumb above the contextual toolbar.
1. Click **Add new service**.
1. Complete the **Create new service** window:
  1. In the **Service name** box, enter a service name.
  1. Leave the **Service type** as **Service**.
1. Click **Accept**.
1. Click **Save** in the toolbar.
1. Click **Edit** in the toolbar.
1. Click **Auto-Start Off** in the toolbar.

## Add Blocks
Before you move on, you're going to want to add some blocks to your project. Blocks can be added in the System Designer or from the command line.

nio blocks are installed to instances using the Block Library. The collection of blocks created by {{ book.product }} is also stored in the [Block Library at blocks.n.io](https://blocks.n.io/). You can search for blocks in the System Designer or in the Block Library.

###To add a block in the System Designer:
1. Click the service name under the instance name in the left navigation panel or on the breadcrumb above the contextual toolbar.
1. In the **Block library** search box, enter a search term.
* If the block is not displayed, click **Available**, **Installed**, and **Configured** to search for the block.
* If the block is not already pre-installed, click the **Install Block** button which resembles a cloud with a down arrow.
1. Drag the block type to the canvas.
1. Name the block.
1. Click **Accept**.

###To add blocks manually:

1. From the project root directory, add the relevant block repository into the `blocks/` folder as a submodule. For example, the logger block:
```
git submodule add https://github.com/nio-blocks/logger.git blocks/logger
```
This can also be done with the nio-cli with `nio add logger`.
1. Restart the System Designer.
1. Click the **Block Library** in the upper-right corner.
1. In the Search box, enter the name of the block. As you type, the list is filtered.
1. Drag the your block onto the canvas.
1. Type the name of the block and click **Accept**.

Once you have {{ book.product }} running, you can create many different projects. To guide you through the process, view the tutorials at https://workshops.n.io/.
