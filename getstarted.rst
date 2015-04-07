Getting Started
===============

Requirements
------------

* `Python 3.4 or greater <https://www.python.org/download/>`_
* `git <http://git-scm.com/download/mac>`_


Installation
------------

We will be installing nio to a virtual environment. This keeps nio and all its dependencies isolated from other python projects and environements you may already have on your machine. You can read more about them `here <https://robinwinslow.co.uk/2013/12/26/python-3-4-virtual-environment/>`_.

First, open a terminal in to the home directory. As a standard we will create a python virtual environement for each nio version.

.. code-block:: bash

    cd
    mkdir nio
    cd nio
    mkdir projects
    mkdir versions
    cd versions
    pyvenv-3.4 1.5.1

Note: that last line will fail with Ubuntu 14.04 but can be fixed with `this <http://askubuntu.com/a/528625>`.

You now need to activate your virtual environment. This will add a `(1.5.1)` to the beginning of your command line to indicate the virtual environemnt that you are using.

.. code-block:: bash

    source 1.5.1/bin/activate

When you're done using nio, you can leave the virtual environment with `deactivate`. When using nio again, be sure to activate the virtual environemtn first with `source ~/nio/versions/1.5.1/bin/activate`.

.. code-block:: bash

    pip install nio-1.5.1-py3-none-any.whl
    pip install nioext-1.5.1-py3-none-any.whl

The installation of nio is now complete! You can run the instance from a project directory with the ``run_nio`` command. See :ref:`setting-up-a-project` for instructions on creating a project directory.

We want to install one more thing before we move on though. We have devloped a Command Line Interface (CLI) to help manage your nio projects.

.. code-block:: bash

    pip install https://github.com/neutralio/nio-cli/archive/master.zip

.. _setting-up-a-project:

Setting up a NIO Project
------------------------

To execute this demo, you'll need `git` (a distributed version control tool) and a `GitHub account <http://github.com>` with `ssh access <https://help.github.com/articles/generating-ssh-keys/#platform-mac>`.

To help you get started, we provide an open source `project template <https://github.com/nio-blocks/project_template>` which reflects the standard directory structure of a nio project. Use the nio CLI to create a new project from the template.

.. code-block:: bash

    cd ~/nio/projects
    nio new getting_started
    cd getting_started

If you don't have ssh access set up for GitHub then try using the https flas:

.. code-block:: bash

    nio new getting_started --https
    
The first thing we're going to need is some blocks. We provide a selection of `open source blocks <https://github.com/nio-blocks>` for your convenience, but, remember, nio is designed to make it easy for you to develop custom blocks; more on this later. For now, let's just get a group of blocks that we've categorized as *util*.

.. code-block:: bash

    nio add util

Again, if you don't have ssh access set up for GitHub then try using the https flas:

.. code-block:: bash

    nio add util --https
    
Some of these blocks have python dependencies, so lets get those installed. (Note: in a future update to the CLI, this will happen automatically).

.. code-block:: bash

    pip install requests

Running nio
~~~~~~~~~~~

This part is simple. With the virtual environment active (which it should already be if you've been following along), run the following command from the root of your project directory (which should also already be ready if you've been following along):

.. code-block:: bash

    cd ~/nio/projects/getting_started
    run_nio

You'll see a bunch of crazy log messages. They should all be INFO messages, so don't worry about those for now. If you see any ERROR messages you may have a problem. But for now lets ignore this one: `NIO [ERROR] [Discover] Failure loading module nioext.components.snmp.agent ImportError:No module named 'pysnmp'`. We won't be using that anyway.

At this point we're don running commands from the terminal, but we will be keeping an eye on these logs.

(Later, when you're done, you'll want to press ctrl-c to exit nio).

Creating your first service
~~~~~~~~~~~~~~~~~~~~~~~~~~~

nio has a web app that you can use to interact with a running nio instance. By default, the `project_template` runs on **127.0.0.1:8181**, so just visit <http://builder.n.io> and log in with the default administrator priviledges (username: Admin; password: Admin). You should see something like this:

.. code-block:: bash

    open http://builder.n.io

.. image:: files/blank_ui.png

To demonstrate the most basic use of the web UI, we'll design a service that generates nio signals automatically and logs them to the nio logging. With the way the `project template` is configured, this means we will see the simulated signals logged to the console and to a log file for our service.

First, click the **Add Service** button that appears in the top-right corner of the center panel of the web UI. Let's name the service `SimulateAndLog`. When you're done entering the service name, click **Submit**. At this point, your browser window should look something like this:

.. image:: files/sim_log_fresh.png

Now we can add a few blocks. The list in the left panel of the UI contains the list of block types currently loaded into nio. Scroll until you find the **Simulator**; click and drag it over to the `SimulateAndLog` grid. Name it `TestSimulator` and click **Submit**. In the left panel, again, scroll to find the **LoggerBlock**, and drag it over to the grid. Name it `TestLogger`.

Click **Save Service** in the bottom right of the right panel (you should get a confirmation that the save was successful).

.. image:: files/sim_log_config.png

Click the **Start Service** button in the very bottom right of the UI, and watch the terminal where you executed **run_nio**.

You should see a bunch of log messages with information about starting and configuring the service, but no signals get logged! This is because we didn't connect the blocks in `SimulateAndLog`. Nio blocks can run in isolation until the cows come home, but they won't communicate with each other until we explicitly connect them. Lets fix that.

First, stop the service (changes to a running service won't be reflected in its behavior until it is restarted anyway). Next, connect `TestSimulator` to `TestLogger`. Click and drag from the dot on the underside of `TestSimulator` to the dot on top of `TestLogger`.

.. image:: files/sim_log_connected.png

Click **Save Service** and **Start Service** again. This time you should see signals logged to the console every second (check the timestamps).

Congratulations! You just built your first nio service!

Configuring blocks
~~~~~~~~~~~~~~~~~~

Lets try changing our service by configuring the blocks to something other than the default behavior.

Click on the `TestSimulator` block to bring up its configuration in the right panel. Don't worry too much about specific properties here. To get familiar though, scroll down to the `Interval` section and change the number in the `Seconds` text box from 1 to 2; click **Save Block**. Now select `TestLogger` in the execution grid and use the drop-down menu to change its `Log Level` and `Log At` to *DEBUG*, saving the block when you're done. 

Restart your service by clicking **Stop Service** and **Start Service**. This time you should see signals logged to the console every 2 seconds (check the timestamps).

Conclusion
~~~~~~~~~~

Now that you've got a nio project with some blocks, try playing around with some of the other blocks. Change some more configuration settings on `TestLogger`. What does `Signal Count do`?. Try putting a **Counter** between a **Simulator** and a **Logger**. All the blocks have `documentation on GitHub <https://github.com/nio-blocks/util>`_.

When you're done with nio, go to the console where your logs are printing and press ctrl-c to exit nio.
