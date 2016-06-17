n.io Blocks
===========

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
