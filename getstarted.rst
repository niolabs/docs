Getting Started
===============

Requirements
------------

* `Python 3.4 or greater <https://www.python.org/download/>`_
* `pip <https://pip.pypa.io/en/latest/installing.html>`_
* virtualenv - ``pip install virtualenv``


Installation
------------

Download the latest nio package from the `nio Downloads Page <http://n.io/download>`_. Once downloaded, expand the zip file and navigate to the directory where it is saved. Then, execute the following commands.

.. code-block:: bash

    $ virtualenv env
    $ source env/bin/activate
    $ pip install -r reqs.txt


The installation of nio is now complete! You can run the instance from a project directory with the ``run_nio`` command. See :ref:`setting-up-a-project` for instructions on creating a project directory.

.. _setting-up-a-project:

Setting up a NIO Project
--------------------

If you already have an existing project configuration, you can skip this section.

To execute this demo, you'll need `git` (a distributed version control tool), a n account with `github <http://github.com>`, and `ruby` (a common scripting language).

To help you get started, we provide an open source `project template <https://github.com/nio-blocks/project_template>` which reflects the standard directory structure of a nio project. Let's begin by cloning down the project template repository into the target directory of your choice:

.. code-block:: bash

    $ cd path/to/nio-projects
    $ git clone https://github.com/nio-blocks/project_template.git
    $ cd project_template
    $ ls
    README.md	blocks		etc		nio.conf
    
The first thing we're going to need is some blocks. We provide a selection of `open source blocks <https://github.com/nio-blocks>` for your convenience, but, remember, nio is designed to make it easy for you to develop custom blocks; more on this later. For now, let's just clone all the repositories in the nio-blocks github organization:

.. code-block:: bash

	$ cd /path/to/project_template/blocks
    $ curl -s https://api.github.com/orgs/nio-blocks/repos?per_page=200 | ruby -rubygems -e 'require "json"; JSON.load(STDIN.read).each { |repo| %x[git clone #{repo["ssh_url"]} ]}'

Some of these blocks contain references to other blocks and **Block Mixins** (which we'll discuss later), which we'll need to initialize. Don't worry too much about this for now; simply copy the following script into your terminal, and git will do all the heavy lifting for you:

.. code-block:: bash

    blocks_dir=`pwd`
    for f in `ls -d */`
    do
        cd $f
        git submodule update --init --recursive
        cd $blocks_dir
    done
    
Now that we have some blocks loaded into the default directory, we can fire up a nio instance and start putting together our first service.
    
.. code-block:: bash    
    
    $ cd /path/to/project_template
    $ run_nio
    <a bunch of log output goes here>
    ...

For now, we host a graphical interface for nio that you can point at a local (or remote) nio instance and run in your browser. By default, the `project_template` runs on **127.0.0.1:8181**, so just visit <http://n.io/builder/?instanceIp=127.0.0.1&instancePort=8181> and log in with the default administrator priviledges (username: Admin; password: Admin). You should see something like this:

.. image:: files/blank_ui.png