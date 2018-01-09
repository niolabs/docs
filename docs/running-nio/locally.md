# Running nio Locally

## Install nio

Make sure to follow the [installation instructions](/installation) first. You will need nio installed on your device before running it.

## Create a Project

Projects are collections of services, blocks and configurations. Create a nio folder to keep things tidy:
```
mkdir -p nio/projects && cd nio/projects
```
Use the nio CLI (Command Line Interface) to create a new project named "my_project":
```
nio new my_project
```
**If you'd rather install the Plant Service from our [Distributed Demostration](https://workshops.n.io/distributed-demonstration/), enter the following:**
```
nio new plant_demo -t plant_demo
```
> You'll be prompted for your Pubkeeper Hostname and Port. To locate these values:
> * Open the **System Designer** in a browser: http://designer.n.io/
> * Select your system in the left hand nav. (To create your first system, follow the instructions [here](https://docs.n.io/getting_started/in_the_cloud.html))
> * Click the **Edit** button in the system toolbar to open its configuration.
> * Enter the values for **hostname** and **token** when prompted.

## Start your Project

```
cd my_project && niod
```
Log messages should display, similar to the following output. There should be no errors.

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

If you see those logs, the nio Platform is up and running. Congratulations!

>By default, new projects use port 8181. If port 8181 isn’t available, you'll see an error. Change the NIOPORT value in your project's nio.env file to fix this error.

>**MacOS Users**: While your system comes pre-installed with Python, it is an older version. When installing newer versions, Python may require that you install and trust a set of Root Certificates for its SSL package. That file is located at /Applications/Python 3.x/Install Certificates.command. Just double-click that file to complete the process. Check /Applications/Python 3.x/ReadMe.rtf for more details.

>The error string you'll see will look something like this:

>```WARNING:tornado.general:SSL Error on 7 ('x.x.x.x', 443): [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed```

Start a nio project from any directory by specifying the project root via the -r flag:
```
niod -r path/to/my_project
```
Run a project in the background on MacOS and Linux using `nohup` (so you can close your terminal):
```
nohup niod -r path/to/my_project 2>&1 > /dev/null &
```

## Add Your Local Instance to the System Designer

To manage your local instance, you need to add it to the **System Designer**:

1. Open the **System Designer** in a browser: http://designer.n.io/
1. Select your system in the left hand nav.
1. Click **create local instance**.
  * In the **instance name** box, enter an instance name.
  * In the **hostname** box, enter **localhost**.
  * In the **port** box, enter **8181**.
  * Leave the **access mode** as **basic**.
1. Click **accept**.

> Note: When the System Designer connects to a nio instance, it communicates with that instance directly from your browser via an XHR request. Hostnames like `localhost` and other internal IP addresses will work. You must have access to the localhost or other IP address from your machine to use the System Designer.
>
>You may see an issue regarding HTTPS and HTTP instances. Since you launched your instance and presumably didn't load any SSL certificates, the instance is accessible only by HTTP. However, if you are logged into the System Designer via HTTPS, your browser will restrict an XHR request going over HTTP. To connect to a local instance, you can log into the designer via HTTP at http://designer.n.io. All of your instances and systems will be the same, except the nio commands to edit these instances won't happen over HTTPS.

Once your instance is loaded and available, you can add services and blocks in the same manner as the [cloud instance](https://docs.n.io/getting-started/in-the-cloud.html#create-service).

Available nio Blocks can be explored in the nio [Block Library](https://blocks.n.io) where you will find a summary of the block's purpose, a list of its properties, commands, inputs, and outputs, and a link to the block code repository.

## View Your Logs

When running in background mode, you can monitor your logs using the “tail” command:
```
tail -f /path/to/my_project/logs/main.log
```

## Stop your Project

```
nio shutdown -p {NIOPORT}
```
> NIOPORT is set in your project's nio.env file
