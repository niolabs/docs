n.io Blocks
===========

What is a block?
--------
A n.io block is a unit of functionality that runs in a service. Some examples of blocks are social media blocks that allow interaction with social media APIs and actuator and sensor blocks which allow various levels of interaction with the real world. These blocks are able to interact with each other through their ability to take signals as input from other blocks and output signals to other blocks. They are also command-able through REST API. Blocks are implemented as python classes.

Block Properties
--------

TODO: Include img of the sidebar where the block properties are configurable.

Syntax
~~~~~~~~
The fields in the configuration sidebar allow python syntax to be used to determine values by enclosing the code in double curly braces.

For example, in order to use the current date in the block configuration, the following python code can be used enclosed in curly braces:
::
{{datetime.datetime.utcnow()}}

The fields of the input signal can also be accessed while using python code by using the '$' operator, and following it with the name of the field. For example, this is how we make a value that uses the a signal with a key of 'size' and value of some integer:
::
{{$size + 1}}

Logging
~~~~~~~~
n.io has logging capabilities that give service makers more information about running n.io services for purposes such as debugging. The **LogLevel** of a block specifies the level of information that is logged when logging information using a logger block. A logger block, logs information about the signal that is passed into the block, including the key-value pairs of the signal.

Block Types
--------
The project template that you get with ``nio new <project-name>`` will get you started with a few block types, but you're going to want to get more. All of the block types that we provide are hosted on GitHub:

.. code-block:: bash

    open https://github.com/nio-blocks

A block repository can contain one or more blocks. For example, ``communication`` includes both the ``Publisher`` and ``Subscriber`` blocks. To add a nio-blocks repository (and all its blocks) to your project, run the following command from the root of your project directory. For example:

.. code-block:: bash

    nio add communication

The n.io CLI supports adding multiple block repositories with one command:

.. code-block:: bash

    nio add communication socketio

Any Python modules in the block's ``requirements.txt`` are ``pip`` installed.

Signals
--------
Signals allow inter-block interaction. They are implemented with a dictionary and as such are a collection of key-value pairs. 

Commands
--------
Block commands can be used through the block API and can be used to interact with blocks that are part of a running service.

Implementation
--------
Block classes have certain methods that must be implemented including process signals, configure, and init. All blocks must also have a version property.
