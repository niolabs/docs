# nio Local Quickstart

The cloud is an easy way to get the nio Platform up and running, but to see the power of nio as a distributed system, you should install and run nio on a locally or at the edge.

>**[info] Requirements**
>
>* **Python3**: https://www.python.org/downloads (you need Python 3.4+)
>* **nio**: https://app.n.io/binaries/download (you'll need to agree to the license)
>  * Windows users should download the Windows Installer. Double-click and follow the prompts.

## Installation

Open a terminal (Applications > Utilities > Terminal on MacOS), and install nio using Python’s pip3 installer (verify the filepath and binary filename below):
```
pip3 install -U ~/Downloads/nio_lite-20180105-py3-none-any.whl
```
> MacOS Users: You may be prompted to install a dependency called "clang". This is a standard component that comes directly from Apple, so it's safe to click "OK" and re-run the command above.

You can test that nio is correctly installed by running the following command:
```
which niod
```
> If you don’t see a path to niod, make sure Python’s binary directory is on your PATH.

> Help setting your PATH: [Windows](https://msdn.microsoft.com/en-us/library/aa922003.aspx) / [MacOS](http://osxdaily.com/2014/08/14/add-new-path-to-path-command-line/).

## Create a Project

Projects are collections of services, blocks and configurations. Create a nio folder to keep things tidy:
```
mkdir -p nio/projects && cd nio/projects
```
Use the nio CLI (Command Line Interface) to create a new project named "my_project":
```
nio new my_project
```
**If you'd rather install the Plant Service from our [Distributed Demostration](https://workshops.n.io/plant/virtual/), enter the following:**
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

> By default, new projects use port 8181. If port 8181 isn’t available, you'll see an error. Change the NIOPORT value in your project's nio.env file to fix this error.

> **MacOS Users**: Python 3.6.4+ requires that you install and trust a set of Root Certificates for Python's SSL package. That file is located at /Applications/Python 3.6/Install Certificates.command. Just double-click that file to complete the process. Check /Applications/Python 3.6/ReadMe.rtf for more details.

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
