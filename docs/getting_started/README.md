# Getting Started #

n.io is a highly scalable open-source stream processing engine. It allows you to asynchronously process streaming data signals and act on them in real-time. It is generally used as the 'brains' of a real-time application, particularly systems that require distributed processing.

Here are a few sample use-cases that n.io could be used for:

- You want to know what people are saying about you on Twitter. Instantaneously get tweets that mention your business, automate responses, identify trends and alert your support team when the number of "help me" tweets passes your acceptable threshold.
- You run a factory or farm and want to optimize workers and the end product. n.io can read from any sensor and act on that data in real-time.
  

In this getting started tutorial you will learn how to get n.io up and running, create a project and build a simple service.

## Basic Concepts ##

Before you install n.io, it's important to understand a few core concepts.

<dl>
  <dt>n.io Binary</dt>
  <dd>Depending on your circumstances, you will run one of many n.io binaries. Binaries range in complexity and are often tuned for hardware. If you're tinkering around on a Raspberry Pi, you don't need to run the same binary as a network of a dozen super computers built to analyze hundreds of thousands signals per second.</dd>
</dl>
<dl>
  <dt>n.io Framework</dt>
  <dd>The n.io library is the versioned portion of the n.io code. You will install the n.io library and then execute that with the appropriate n.io binary. Install the framework with pip: ``pip install n.io``.</dd>
</dl>
<dl>
  <dt>Project</dt>
  <dd>A n.io project is a directory on your computer that contains all the configuration that defines your n.io implementation. Projects can run stand-alone or they can be a part of a larger n.io network where many n.io instances communicate with one another.</dd>
</dl>
<dl>
  <dt>Service</dt>
  <dd>A service is a runnable piece of n.io that defines your application logic. Services define how blocks are connected together.</dd>
</dl>
<dl>
  <dt>Block</dt>
  <dd>A block is a configurable piece of code that processes data signals. Blocks can generate signals and/or consume signals.</dd>
</dl>
<dl>
  <dt>Signal</dt>
  <dd>A signal is a unit of data that is passed from block to block within a service. Think of it is a little box of data, containing anything from a temperature reading to a tweet.</dd>
</dl>
## Installation ##

n.io requires at least Python 3.4. You will also need pip to install n.io and its dependencies. Finally, n.io projects are best managed using git and in this tutorial you'll be pulling down a project template from GitHub. Before you install n.io, make sure you have all these things:

<dl>
  <dt>    python3 --version</dt>
  <dd>
    <p>python3 --version</p>
    <p>pip3 --version</p>
    <p>git --version</p>
  </dd>
</dl>
Once you have these basic prerequisites, you can download and install n.io. The binaries are not necessarily publicly available, so if you don't have a wheel to install, you better make friends with someone who does! You may need to ``sudo`` install if the following doesn't work for you:

    pip3 install <n.io-binary.whl>

<dl>
  <dt>.. note :  : </dt>
  <dd>Depending on how ``pip`` was installed, the command may be slightly different. You can verify the command to call pip by trying ``pip``, ``pip3``, or ``pip3.4`` with the ``--version`` option. Also, if you have access to the web hosted n.io wheels, you can use ``pip3.4 install http://<URL-of-n.io-wheels>``.</dd>
</dl>
Now we're going to install the n.io CLI. While not required to run n.io, it is helpful for setting up a project and running it:

    pip3 install n.io-cli

## Creating and Running a Project ##

Alright, now it's time for things to get interesting. Create a n.io project in your current directory using the CLI we just installed:

    n.io new first_project

This will create a new folder in your current directory called ``first_project`` containing the contents of the default project pulled from GitHub. You can poke around in the project directory but when you are ready to launch n.io head into the project root (``cd first_project`` if you are in your original working directory) and then execute n.io. You can use the CLI to launch n.io, or if your binary came with a custom executable name, run that.

Using a custom executable (i.e. ``n.io_run``):

    n.io_run

Using the CLI (if your binary didn't come with a custom executable):

    n.io server

If all goes well, you should see something like the following logs:

<dl>
  <dt>    [2016-03-04 23 : 49 : 41.035] NIO [INFO] [main.WebServer] Server configured on 0.0.0.0 : 8181</dt>
  <dd>
    <p>[2016-03-04 23:49:41.035] NIO [INFO] [main.WebServer] Server configured on 0.0.0.0:8181</p>
    <p>[2016-03-04 23:49:41.042] NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from:  to: created</p>
    <p>[2016-03-04 23:49:41.055] NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from: created to: configuring</p>
    <p>[2016-03-04 23:49:41.109] NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from: configuring to: configured</p>
    <p>[2016-03-04 23:49:41.123] NIO [INFO] [main.WebServer] Starting server on 0.0.0.0:8181</p>
    <p>[2016-03-04 23:49:41.226] NIO [INFO] [main.WebServer] Server 0.0.0.0:8181 started on 0.0.0.0:8181</p>
    <p>[2016-03-04 23:49:41.226] NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from: configured to: starting</p>
    <p>[2016-03-04 23:49:41.227] NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from: starting to: started</p>
  </dd>
</dl>
You can see that we now have a web server running on port 8181. This is how you will communicate with n.io. Open up a new terminal window and verify that you can access the api by hitting the /n.io endpoint:

    curl localhost:8181/n.io

### Adding Blocks to a Project ###

Before we move on, you're going to want to add some blocks to your project. Press ctrl-c to ext n.io. We'll add four popular blocks to get you started:

    n.io add logger simulator filter dynamic_fields

## Explore n.io ##

If you don't have n.io running already, do that now:

    n.io_run

### System Designer ###

While we could continue using the REST API directly, we don't need to do that in this tutorial. Instead, we'll use this handy web app:

    open http://designer.n.io

First you will need to create a system to run your n.io project. Click on the '+' icon on the left of the screen and give your system a name (i.e. local).

Now you will need to add an instance to your service. We will make a local instance and not a cloud instance so click on the "add new instance" button at the top of the screen. Give your instance a name, set the host name to "localhost", change the port number to 8181, and click "accept". Now you can enter your instance canvas.

It's looking pretty empty in there so we will need to create a service. While it won't get too exciting quite yet, we'll start by building a very basic service to simulate and log signals. By default, the projects logs go to standard out as well as to files in the ``logs`` directory of your project folder.

Start by clicking the "add new service" button and name your service "SimulateAndLog".

Now that we have a service, we'll add a CounterIntervalSimulator block and a Logger block. Double click on your "SimulateAndLog" service. From the right, click on "LB" and drag a LoggerBlock onto the service canvas. Go ahead give it the name "Log". Do the same with "CIS" and drag in a CounterIntervalSimulator and name it "Simulate".

Now connect these blocks by clicking and dragging on the output terminal of "Simulate" and release it on the input terminal of "Log".

Once you are satisfied with your service, click the "save" icon at the top of the instance canvas.

### Running Services ###

By now I'm sure you're more than ready to see something happen. Click the "start" icon from the top of the service canvas and you should see some logs appear in the terminal where you ran n.io from.

<dl>
  <dt>    [2016-03-05 00 : 32 : 05.189] NIO [INFO] [SimulateAndLog.Log] Block : Log (type : LoggerBlock) status is configured</dt>
  <dd>
    <p>[2016-03-05 00:32:05.189] NIO [INFO] [SimulateAndLog.Log] Block: Log (type: LoggerBlock) status is configured</p>
    <p>[2016-03-05 00:32:05.191] NIO [INFO] [SimulateAndLog.service] Service: SimulateAndLog status changed from: configuring to: configured</p>
    <p>[2016-03-05 00:32:05.193] NIO [INFO] [SimulateAndLog.service] Service: SimulateAndLog status changed from: configured to: starting</p>
    <p>[2016-03-05 00:32:05.199] NIO [INFO] [SimulateAndLog.Log] Block: Log (type: LoggerBlock) status is starting</p>
    <p>[2016-03-05 00:32:05.199] NIO [INFO] [SimulateAndLog.Log] Block: Log (type: LoggerBlock) status is started</p>
    <p>[2016-03-05 00:32:05.200] NIO [INFO] [SimulateAndLog.service] Service: SimulateAndLog status changed from: starting to: started</p>
    <p>[2016-03-05 00:32:05.200] NIO [INFO] [SimulateAndLog.Log] {'sim': 0}</p>
    <p>[2016-03-05 00:32:05.201] NIO [INFO] [main.ServiceManager] Service: SimulateAndLog with process identifier(pid): 65638 has started</p>
    <p>[2016-03-05 00:32:06.203] NIO [INFO] [SimulateAndLog.Log] {'sim': 1}</p>
    <p>[2016-03-05 00:32:07.204] NIO [INFO] [SimulateAndLog.Log] {'sim': 0}</p>
    <p>[2016-03-05 00:32:08.204] NIO [INFO] [SimulateAndLog.Log] {'sim': 1}</p>
    <p>[2016-03-05 00:32:09.203] NIO [INFO] [SimulateAndLog.Log] {'sim': 0}</p>
    <p>[2016-03-05 00:32:10.204] NIO [INFO] [SimulateAndLog.Log] {'sim': 1}</p>
  </dd>
</dl>
Click the "stop" icon when you're ready to move on.

### Configuring Blocks ###

So far we're only using the default behavior of these blocks. Why don't you try changing things up by configuring the Simulate block. Click on the top right of the block and take a look at it's properties on the pop out menu. You'll notice that Interval is configured to 1 second. Change that to 2 and then click "save". Now when you start the service, you'll only see signals logged every other second.

### Commanding Blocks and Services ###

Commands are a way to execute code in a block or service. Technically, you've already commanded services with "start" and "stop".

Running blocks can also be commanded. With the SimulateAndLog service running, select the Log block and then click the "command" button from the menu. Select "log", type in a phrase and then click "execute". You'll see your phrase logged alongside the simulated signals.

## Conclusion ##

At this point you should feel comfortable installing n.io, creating a project with blocks and configuring and running services. You can find block `documentation on GitHub <https://github.com/n.io-blocks>`_.
