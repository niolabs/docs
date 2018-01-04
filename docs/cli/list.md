# List


When called without a specific block or service name, this subcommand lists all the blocks or services loaded in the instance along with a common subset of properties:
.. code-block:: bash**
    $ nio ls blocks
    +----------------+--------------+-----------+
    |      name      |     type     | log_level |
    +----------------+--------------+-----------+
    | Deb            |  Debouncer   |   ERROR   |
    | fil            |    Filter    |   ERROR   |
    | PostToMe       |  PostSignal  |   DEBUG   |
    | CountMe        |   Counter    |   ERROR   |
    | count          |   Counter    |   ERROR   |
    | FacebookPoster | FacebookPost |   ERROR   |
    | TwitterPoster  | TwitterPost  |   DEBUG   |
    | SignalLogger   | LoggerBlock  |   DEBUG   |
    +----------------+--------------+-----------+

When called with a block or service name, **nio** outputs a list of all the properties on that block or service:
.. code-block:: bash
    $ nio ls blocks TwitterPoster
    +------------------------+----------------------------------------------------+
    | TwitterPoster          |                                                    |
    +------------------------+----------------------------------------------------+
    | creds                  |                                                    |
    | +-> oauth_token        |                XXXXXXXXXXXXXXXXXXX                 |
    | +-> consumer_key       |                XXXXXXXXXXXXXXXXXXX                 |
    | +-> oauth_token_secret |                XXXXXXXXXXXXXXXXXXX                 |
    | +-> app_secret         |                XXXXXXXXXXXXXXXXXXX                 |
    | log_level              |                       DEBUG                        |
    | status                 |                 What the {{$foo}}?                 |
    | type                   |                    TwitterPost                     |
    +------------------------+----------------------------------------------------+

To list the HTTP commands (with enumerated parameters) exposed by a particular block or service, simply append the '--cmd' flag:
.. code-block:: bash
    $ nio ls services TestPost --cmd
    +---------+------------------+
    | command |        0         |
    +---------+------------------+
    | log     | phrase: (string) |
    +---------+------------------+

To view the block execution of a particular service (in tabular form), append the '--exec' flag:
.. code-block:: bash
    $ nio ls services SomeService --exec
    +--------------+--------------+
    | Output Block |      0       |
    +--------------+--------------+
    |     met      | SignalLogger |
    |   CountMe    |     Deb      |
    |     Deb      | SignalLogger |
    |   PostToMe   |   CountMe    |
    +--------------+--------------+
