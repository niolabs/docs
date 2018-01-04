# Config

This subcommand allows you to configure new and existing block and service instances while the NIO instance is live. Of course, a given service won't load a new configuration until its next startup cycle, but any changes you make here will hang around until then. Note that this is an interactive portion of the utility.
NB: If you want to automate configuration, it may be easier to make your updates directly via HTTP PUT requests. We may add a feature like this in future.
.. code-block:: bash
    $ nio cfg services TestPost

    log_level (select):
    Using current value: DEBUG

    auto_start (bool): T

If the block or service you're configuring holds an Object Property, each property held by that object is configured in turn:
.. code-block:: bash
    $ nio cfg blocks TwitterPoster

    creds (object):
    +->oauth_token (str):
    Using current value: XXXXXXXX
    +->consumer_key (str):
    Using current value: XXXXXXXX
    +->app_secret (str):
    Using current value: XXXXXXXX
    +->oauth_token_secret (str):
    Using current value: XXXXXXXX
    status (str): "It's gonna rain"
    log_level (select):
    Using current value: DEBUG

`nio` interprets attempts to configure nonexistent resources as creation events. That is, the following sequence results in the creation of a block called "CriticalLogger", which can subsequently be added to any service execution in the system.
.. code-block:: bash
    $ nio cfg blocks AnotherLogger
    NIOClient: NIO returned status 404
    type (str): LoggerBlock
    log_level (select): CRITICAL
    +----------------------+-------------+
    | Name: CriticalLogger |             |
    +----------------------+-------------+
    | log_level            |   CRITICAL  |
    | type                 | LoggerBlock |
    +----------------------+-------------+

Currently, NIO ships with only one service type (`Service`), but developers are free to add both new blocks and services as they wish.
