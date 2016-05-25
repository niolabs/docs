Additional APIs
===============

Nio has some additional APIs that you may find useful as you explore what nio has to offer.

Configuration Refresh API
-------------------------

The ``/config/refresh`` endpoint is used when you update block or service configuration files through some means outside of the n.io ``blocks`` and ``services`` APIs. For example, if you use a text editor to modify a block configuration file, you will need to tell a running n.io instance to use those changes:

.. code-block:: bash

    curl -XGET 'localhost:8181/config/refresh' --user 'Admin:Admin'
