Builder
=======

The easiest way to interact with a running n.io instance is with our web app, lovingly referred to as ``The Builder``:

.. code-block:: bash

    open http://builder.n.io

Essentially, the builder is simply a graphical user interface that interacts with n.io through the REST API.

Getting to know your way around
-------------------------------

The builder is split up into three columns. Let's take a look at each one, from left to right.

Block Types
~~~~~~~~~~~

The left hand column shows you all the block types that are included in the project and any configured instances of those blocks. Clicking the ``+`` sign will expand the block type to reveal any block instances of that type.

When you add a new block type (``nio add <block>``) or upgrade a block (``nio add <block> --upgrade``) in an already running instance of n.io, you'll need to tell n.io about that so that you can use them. The ``Add Block`` and ``Reload Block`` buttons allow you to do this. You can alternatively restart your n.io instance, which will always start up with the affects of your ``nio add`` commands.

Services
~~~~~~~~

The middle column is where you see all the services for the project. This is also where you view and configure your services.

On the ``Service List`` tab you get a highlevel view of the services. On the left you will see a red rectangle for stopped services and a green rectangle for started services. Services in any other state are white (example: error state). A few buttons are available for some interaction:

* ``Start`` and ``Stop`` a service.
* ``Clone``. Create a copy of the service with a new name.
* ``Modify``. Enable modification of the ``Auto start`` flag. When this flag is ``ON``, the service starts automatically when the n.io projects starts.
* ``Delete`` a service.

Clicking on a service opens up a new tab where you can see the block execution of that service. From here you can drag blocks from the ``Block Types`` column onto a service. When you click on a block type and drag it onto the service, it will create a new block of that type and you will be prompted to give that block a name. To reuse an already created block, instead drag a block from the expanded ``+`` list onto the service. To connect blocks together, click on the output terminal of a block and drag the arrow to the input terminal of another block.

Block Configuration and Control Buttons
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The right hand column is where you configure your blocks. After clicking on a block in either the ``Block Types`` section of the builder of a block in a service, you see the configuration of the block here. View and edit the properties here. Remember that if a block is used in multiple places (either within one service or in multiple services), edits to that block will happen to all uses of it.

The bottom right corner is where you can save, copy and delete blocks and services. Nothing in the builder is auto-saved. Before clicking away from a block, you must click ``Save Block``. After making changes to a service, make sure to click ``Save Service`` before ``Start Service`` or your changes will not take affect.

The ``Command Block`` button is used to run block commands on blocks in a running service.

Block Commands
--------------

Some block types have commands than can be executed on running blocks. The ``Command Block`` button opens a window where you can execute these commands and see the results returned by them. Some commands are simply to view current information about running block but others will affect the running instance, perhaps by clearing or setting some variable in the block.

Accessing remote n.io instances
-------------------------------

By default, the builder will look for a project running on your local machine on the port ``8181``. If you are looking to the builder up for some other n.io instance, you the ``instanceIp`` and ``instancePort`` URL arguments.

.. code-block:: bash

    open http://builder.n.io/?instanceIp=192.168.1.1&instancePort=8182

User Authentication
-------------------

The bottom left is where you log in and out of the builder. When using a n.io instance with Basic Authentication, check the ``Basic?`` box. For OAuth n.io instances, logging into the builder with a Google account that has access to the instance is enough.
