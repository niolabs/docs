# Running nio Locally

The cloud is an easy way to get nio up and running, but doesn't fully encapsulate the distributed power of the nio platform. Instead, you should run nio on a local or edge node.  In this guide, you will create a local instance that uses a cloud-based Pubkeeper server to handle communications.

Running the nio platform requires Python version 3.4 or greater.

Requirements

* Download Python 3.4 or greater from [https://www.python.org/downloads/](https://www.python.org/downloads/).
* Obtain the nio binary Python wheel file (`.whl`) with your license agreement.

## Download nio

Download nio from the following URL:

https://app.n.io/binaries/download

## Install the nio binary and CLI

To install nio, enter the following command:
```
pip3 install your_wheel_file.whl
```

To install the nio Command Line Interface \(CLI\), enter the following command:
```
pip3 install nio-cli
```

## Upgrade the nio binary and CLI

To upgrade nio, enter the following command:
```
pip3 install -U your_wheel_file.whl
```

To upgrade the nio CLI, enter the following command:
```
pip3 install -U nio-cli
```

## Create a Project

Now that you have the nio binary to run, you need a nio [project](https://docs.n.io/glossary/#project) to run it with. Obtain a nio project template by using the nio CLI or by cloning the [Project Template repository](https://github.com/niolabs/project_template) from Github directly.

### Download using the nio CLI
To clone the project template using CLI, enter the following command:

`nio new first_project`

The `first_project` directory is created in your working directory containing the nio project.

### Download using Git
To clone the project template using Git, clone the template, and initialize the submodules which contain the blocks.
```
git clone https://github.com/niolabs/project_template.git first_project
cd first_project
git submodule update --init --recursive
```

## Set up nio environment

After adding the new project, change to the project directory
```
cd first_project
```
## Create a System
When you first open the **System Designer**, you will see your canvas. The canvas is where you will build [systems](https://docs.n.io/glossary#system) containing instances, services, and blocks. To begin, create a system that will contain projects you create as you learn to use nio.

1. Open the **System Designer** in a new tab in your browser.

  https://designer.n.io/

1. You can create a new system in two ways.
  * If this is your first time opening nio, the **create new system** window displays.

    %accordion%**Click arrow to collapse/expand**%accordion%

    ![](/img/CreateNewSystem.png)

    %/accordion%

  * If you have already been working in nio, in the lower-left corner, click the **`+`** button.

    %accordion%**Click arrow to collapse/expand**%accordion%

    ![](/img/BlankCanvas.png)

    %/accordion%
1. Complete the **create new system** window:
  1. In the **system name** box, enter your system name.
  1. Click **accept**.
1. Click **edit** in the contextual toolbar to open the system's configuration.
> Make note of the values for **hostname** and **token** which will be used in the following steps.
1. From your terminal, in your first_project directory, open the `nio.env` file.
1. Update the following four lines in the `# Pubkeeper Client` section
```
PK_HOST: [your copied host]
PK_PORT: 443
PK_TOKEN: [your copied token]
PK_SECURE: True
```
1. Update the following three lines in the `# Websocket Brew Variables` section
```
WS_HOST: [your copied host, replacing `pubkeeper` with `websocket`]
WS_PORT: 443
WS_SECURE: True
```

1. To run nio, enter the following command:
```
nio_run
```
> If that command is not available, make sure your Python binary installation directory is on your PATH.

  * If you need help setting your PATH in Windows, click [here](https://msdn.microsoft.com/en-us/library/aa922003.aspx).
  * If you need help setting your PATH in MacOS, click [here](http://osxdaily.com/2014/08/14/add-new-path-to-path-command-line/).

1. You should see log messages display similar to the following output.

  ```
  NIO [INFO] [main.WebServer] Server configured on 0.0.0.0:8181
  NIO [INFO] [main.WebServer] Server configured on 0.0.0.0:8181
  NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from:
    to: created
  NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from:
    created to: configuring
  NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from:
    configuring to: configured
  NIO [INFO] [main.WebServer] Starting server on 0.0.0.0:8181
  NIO [INFO] [main.WebServer] Server 0.0.0.0:8181 started on 0.0.0.0:8181
  NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from:
    configured to: starting
  NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from:
    starting to: started
  ```

If you see those logs, nio is up and running. Congratulations!

## Add a Local Instance

Once you have a local [instance](https://docs.n.io/glossary#instance) running, you can edit it using the **System Designer**. Based on the log messages, your nio instance is available at `http://localhost:8181` and you need basic authentication to communicate with the instance.

1. Select the name of your system in the left navigation panel or on the breadcrumb above the contextual toolbar.

  ![](/img/hierarchy.gif)
1. Click **create local instance**.
1. Complete the **create local instance** window:
  * In the **instance name** box, enter your instance name.
  * In the **hostname** box, enter **localhost**.
  * In the **port** box, enter **8181**.
  * Leave the **access mode** as **basic**.
1. Click **accept**.
1. Wait for the instance to spin-up and note the name of the new instance on the left.

  >Note: When you connect to a nio instance, you are communicating with that instance directly from your browser via an XHR request. Hostnames like `localhost` and other internal IP addresses will work. You must have access to the localhost or other IP address from your machine to use the **System Designer**.

You may see an issue regarding HTTPS and HTTP instances. Since you launched your instance and presumably didn't load any SSL certificates, the instance is accessible only by HTTP. However, if you are logged into the **System Designer** via HTTPS, then an XHR request going over HTTP is not permitted due to a browser restriction. Instead, log into the designer via HTTP. All of your instances and systems will be the same, except the nio commands to edit these instances won't happen over HTTPS.

Once your instance is loaded and available, you can add [services](https://docs.n.io/glossary#service) and [blocks](https://docs.n.io/glossary#block) in the same manner as the cloud instance. You can view any errors or activity from the logs in your terminal that is running nio. When you need to debug a system, a local instance is a useful tool.

Once you have nio running, you can create many different projects. To guide you through the process, view the tutorials at https://workshops.n.io/.
