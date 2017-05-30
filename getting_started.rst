Getting Started
===============

Nio is a highly scalable open-source stream processing engine. It allows you to asynchronously process streaming data signals and act on them in real-time. It is generally used as the 'brains' of a real-time application, particularly systems that require distributed processing.

Here are a few sample use-cases that nio could be used for:

* You want to know what people are saying about you on Twitter. Instantaneously get tweets that mention your business, automate responses, identify trends and alert your support team when the number of "help me" tweets passes your acceptable threshold.
* You run a factory or farm and want to optimize workers and the end product. Nio can read from any sensor and act on that data in real-time.

In this getting started tutorial you will learn how to get nio up and running, create a project and build a simple service.

Basic Concepts
--------------

Before you install nio, it's important to understand a few core concepts.

Project
  A nio project is a directory on your computer that contains all the configuration that defines your nio implementation. Projects can run stand-alone or they can be a part of a larger nio network where many nio instances communicate with one another.
Block
  A block is a configurable piece of code that processes data signals. Blocks can generate signals and/or consume signals.
Service
  A service is a runnable piece of nio that defines your application logic. Services define how blocks are connected together.
Signal
  A signal is a unit of data that is passed from block to block within a service. Think of it is a little box of data, containing anything from a temperature reading to a tweet.
Nio Framework
  The nio library is the versioned portion of the nio code. You will install the nio library and then execute that with the appropriate nio binary. Install the framework with pip: ``pip install nio``.
Nio Binary
  Depending on your circumstances, you will run one of many nio binaries. Binaries range in complexity and are often tuned for hardware. If you're tinkering around on a Raspberry Pi, you don't need to run the same binary as a network of a dozen super computers built to analyze hundreds of thousands signals per second.

Installation
------------

Nio requires at least Python 3.4. You will also need pip to install nio and its dependencies. Finally, nio projects are best managed using git and in this tutorial you'll be pulling down a project template from GitHub. Before you install nio, make sure you have all these things:

.. code-block:: bash

    python3 --version
    pip3 --version
    git --version

Once you have these basic prerequisites, you can download and install nio. The binaries are not necessarily publicly available, so if you don't have a wheel to install, you better make friends with someone who does! You may need to ``sudo`` install if the following doesn't work for you:

.. code-block:: bash

    pip3 install <nio-binary.whl>

.. note::

    Depending on how ``pip`` was installed, the command may be slightly different. You can verify the command to call pip by trying ``pip``, ``pip3``, or ``pip3.4`` with the ``--version`` option. Also, if you have access to the web hosted nio wheels, you can use ``pip3.4 install http://<URL-of-nio-wheels>``.

Now we're going to install the Nio CLI. While not required to run Nio, it is helpful for setting up a project and running it:

.. code-block:: bash

    pip3 install nio-cli

Creating and Running a Project
------------------------------

Alright, now it's time for things to get interesting. Create a Nio project in your current directory using the CLI we just installed:

.. code-block:: bash

    nio new first_project

This will create a new folder in your current directory called ``first_project`` containing the contents of the default project pulled from GitHub. You can poke around in the project directory but when you are ready to launch n.io head into the project root (``cd first_project`` if you are in your original working directory) and then execute n.io. You can use the CLI to launch n.io, or if your binary came with a custom executable name, run that.

Using the CLI (if your binary didn't come with a custom executable):

.. code-block:: bash

    nio server

Using a custom executable (i.e. ``nio_pi``):

.. code-block:: bash

    nio_pi

If all goes well, you should see something like the following logs:

TODO: update logs for 2.x

.. code-block:: bash

    [2016-03-04 23:49:41.035] NIO [INFO] [main.WebServer] Server configured on 0.0.0.0:8181
    [2016-03-04 23:49:41.042] NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from:  to: created
    [2016-03-04 23:49:41.055] NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from: created to: configuring
    [2016-03-04 23:49:41.109] NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from: configuring to: configured
    [2016-03-04 23:49:41.123] NIO [INFO] [main.WebServer] Starting server on 0.0.0.0:8181
    [2016-03-04 23:49:41.226] NIO [INFO] [main.WebServer] Server 0.0.0.0:8181 started on 0.0.0.0:8181
    [2016-03-04 23:49:41.226] NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from: configured to: starting
    [2016-03-04 23:49:41.227] NIO [INFO] [main.ServiceManager] Component: ServiceManager status changed from: starting to: started

You can see that we now have a web server running on port 8181. This is how you will communicate with Nio. Open up a new terminal window and verify that you can access the api by hitting the /nio endpoint:

.. code-block:: bash

    curl localhost:8181/nio

Adding Blocks to a Project
~~~~~~~~~~~~~~~~~~~~~~~~~~

Before we move on, you're going to want to add some blocks to your project. Press ctrl-c to ext nio. We'll add four popular blocks to get you started:

.. code-block:: bash

    nio add logger simulator filter dynamic_fields

.. note::

    **Using n.io 2.0?**

    For n.io 2.0 you will have to update your blocks to the ``nio2`` branch. By default, the CLI will put the blocks on the master branch. To switch your blocks to the ``nio2`` branch you can run this git command, or manually go into each block folder and checkout the branch.

    .. code-block:: bash

        git submodule foreach git checkout nio2

    If a block doesn't have a ``nio2`` branch it means it hasn't been converted to 2.0 yet. Unfortunately, n.io 1.x blocks are not compatible with the n.io 2.x framework.

Explore Nio
-----------

If you don't have Nio running already, do that now:

.. code-block:: bash

    nio_run

Designer
~~~~~~~

While we could continue using the REST API directly, we don't need to do that in this tutorial. Instead, we'll use this handy web app:

.. code-block:: bash

    open http://designer.n.io


It's looking pretty empty in there but you should at least see a list of blocks on the left. While it won't get too exciting quite yet, we'll start by building a very basic service to simulate and log signals. By default, the projects logs go to standard out as well as to files in the ``logs`` directory of your project folder.

Start by clicking the "add new service" button and name your service "SimulateAndLog".

Now that we have a service, we'll add a CounterIntervalSimulator block and a Logger block. Double click on your "SimulateAndLog" service. From the right, click on "LB" and drag a LoggerBlock onto the service canvas. Go ahead give it the name "Log". Do the same with "CIS" and drag in a CounterIntervalSimulator and name it "Simulate".

Now connect these blocks by clicking and dragging on the output terminal of "Simulate" and release it on the input terminal of "Log".

Once you are satisfied with your service, click the "save" icon at the top of the instance canvas.

Running Services
~~~~~~~~~~~~~~~~

By now I'm sure you're more than ready to see something happen. Click the "start" icon from the top of the service canvas and you should see some logs appear in the terminal where you ran nio from.

.. code-block:: bash

    [2016-03-05 00:32:05.189] NIO [INFO] [SimulateAndLog.Log] Block: Log (type: LoggerBlock) status is configured
    [2016-03-05 00:32:05.191] NIO [INFO] [SimulateAndLog.service] Service: SimulateAndLog status changed from: configuring to: configured
    [2016-03-05 00:32:05.193] NIO [INFO] [SimulateAndLog.service] Service: SimulateAndLog status changed from: configured to: starting
    [2016-03-05 00:32:05.199] NIO [INFO] [SimulateAndLog.Log] Block: Log (type: LoggerBlock) status is starting
    [2016-03-05 00:32:05.199] NIO [INFO] [SimulateAndLog.Log] Block: Log (type: LoggerBlock) status is started
    [2016-03-05 00:32:05.200] NIO [INFO] [SimulateAndLog.service] Service: SimulateAndLog status changed from: starting to: started
    [2016-03-05 00:32:05.200] NIO [INFO] [SimulateAndLog.Log] {'sim': 0}
    [2016-03-05 00:32:05.201] NIO [INFO] [main.ServiceManager] Service: SimulateAndLog with process identifier(pid): 65638 has started
    [2016-03-05 00:32:06.203] NIO [INFO] [SimulateAndLog.Log] {'sim': 1}
    [2016-03-05 00:32:07.204] NIO [INFO] [SimulateAndLog.Log] {'sim': 0}
    [2016-03-05 00:32:08.204] NIO [INFO] [SimulateAndLog.Log] {'sim': 1}
    [2016-03-05 00:32:09.203] NIO [INFO] [SimulateAndLog.Log] {'sim': 0}
    [2016-03-05 00:32:10.204] NIO [INFO] [SimulateAndLog.Log] {'sim': 1}

Click the "stop" icon when you're ready to move on.

Configuring Blocks
~~~~~~~~~~~~~~~~~~

So far we're only using the default behavior of these blocks. Why don't you try changing things up by configuring the Simulate block. Click on the top right of the block and take a look at it's properties on the pop out menu. You'll notice that Interval is configured to 1 second. Change that to 2 and then click "save". Now when you start the service, you'll only see signals logged every other second.

Commanding Blocks and Services
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Commands are a way to execute code in a block or service. Technically, you've already commanded services with "start" and "stop".

Running blocks can also be commanded. With the SimulateAndLog service running, select the Log block and then click the "command" button from the menu. Select "log", type in a phrase and then click "execute". You'll see your phrase logged alongside the simulated signals.

Conclusion
----------

At this point you should feel comfortable installing nio, creating a project with blocks and configuring and running services. You can find block `documentation on GitHub <https://github.com/nio-blocks>`_.
