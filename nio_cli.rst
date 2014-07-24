NIO Command Line Tools
======================

nio-instance
-----------

NIO exposes a rich API for interacting with running instances. We provide a robust browser-based graphical user interface to same, but such interfaces are rarely well suited to automation of tasks and rapid context switching. For this reason, we provide the **nio-instance** command line tool, which allows users and administrators to start, stop, view, configure, and build blocks and services from a UNIX command line.

Here's an example:

.. code-block:: bash

    $ nio-instance ls services TestPost
    +--------------+---------+
    | TestPost     |         |
    +--------------+---------+
    | auto_start   |   True  |
    | log_level    |  DEBUG  |
    | mappings     |   NULL  |
    | sys_metadata |   NULL  |
    | type         | Service |
    +--------------+---------+

**nio-instance** is configurable by python `.ini` file. By default, it looks in `$HOME/.config/nio-cli.ini` under the section **nio-instance** for a hostname, port, username, and password. The path to the `.ini` file is configurable by command-line option, but make sure you put all the **nio-instance** options under the appropriate section. Here's an example:

.. code-block:: conf

    [DEFAULT]
    host = localhost
    port = 8181
    username = User
    password = User
    
    [nio-instance]
    username = Admin
    password = Admin
    
**nio-instance** exposes a number of sub-commands to perform various tasks. Each, and its syntax, is represented by one of the following subsections.

list (ls)
~~~~~~~~~

When called without a specific block or service name, this subcommand lists all the blocks or services loaded in the instance along with a common subset of properties:

.. code-block:: bash**

	$ nio-instance ls blocks
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
	
When called with a block or service name, **nio-instance** outputs a list of all the properties on that block or service:

.. code-block:: bash

    $ nio-instance ls blocks TwitterPoster
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

   	$ nio-instance ls services TestPost --cmd
   	+---------+------------------+
	| command |        0         |
	+---------+------------------+
	| log     | phrase: (string) |
	+---------+------------------+
   	
	
command (co)
~~~~~~~~~~~~

This subcommand allows you to send commands to live instances. Because of the way blocks are referenced within NIO, you must supply the target command, the name of the service, and (if you are commanding a block) the name of the block instance.

.. code-block:: bash

	$ nio-instance co start TestPost
	`http://localhost:8181/services/TestPost//start` was processed successfully
	
The syntax for adding parameters to commands is as follows:

.. code-block:: bash
	
	$ nio-instance co log TestPost SignalLogger --args 'phrase=foobar'
	
Passing the `--interactive` (`-i`) flag to command tells **nio-instance** to prompt you for command parameters.
	
If the command response body is non-empty, its contents are printed to stdout. Otherwise, the terminal remains silent.

config (cfg)
~~~~~~~~~~~~

This subcommand allows you to configure block and service properties while the instance is live. Of course, a given service won't load a new configuration until its next startup cycle, but any changes you make here will hang around until then. Note that this is an interactive portion of the utility. If you'd like to leave the 

NB: If you want to automate configuration, it may be easier to make your updates directly via HTTP PUT requests. We may add a feature like this in future.

.. code-block:: bash

    $ nio-instance cfg services TestPost
    
    log_level (select):
    Using current value: DEBUG
    
    auto_start (bool): T
    
If the block or service you're configuring holds an Object Property, each property held by that object is configured in turn:

.. code-block:: bash

    $ nio-instance cfg blocks TwitterPoster
    
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
    



build (ln)
~~~~~~~~~

This final subcommand allows you to build NIO services from the command line by creating links between blocks that are loaded into the sytem. Calling this subcommand on a service with no other arguments produces a tabular representation of that service's execution.

.. code-block:: bash

    $ nio-instance build TestPost
    +--------------+--------------+
    | Output Block |      0       |
    +--------------+--------------+
    |     met      | SignalLogger |
    |   CountMe    |     Deb      |
    |     Deb      | SignalLogger |
    |   PostToMe   |   CountMe    |
    +--------------+--------------+
    
Let's use `ls` to grab the list of available blocks and use `build` to send the output of `CountMe` to another block!

.. code-block:: bash

    $ nio-instance ls blocks
    +----------------+--------------+-----------+
    | name           |     type     | log_level |
    +----------------+--------------+-----------+
    | count          |   Counter    |   ERROR   |
    | met            |   Metrics    |   ERROR   |
    | SignalLogger   | LoggerBlock  |   DEBUG   |
    | PostToMe       |  PostSignal  |   DEBUG   |
    | Deb            |  Debouncer   |   ERROR   |
    | FacebookPoster | FacebookPost |   ERROR   |
    | CountMe        |   Counter    |   ERROR   |
    | fil            |    Filter    |   ERROR   |
    | TwitterPoster  | TwitterPost  |   DEBUG   |
    +----------------+--------------+-----------+
    
    $ nio-instance build TestPost 'CountMe=>TwitterPoster'
    +--------------+--------------+---------------+
    | Output Block |      0       |       1       |
    +--------------+--------------+---------------+
    |   CountMe    |     Deb      | TwitterPoster |
    |     met      | SignalLogger |               |
    |   PostToMe   |   CountMe    |               |
    |     Deb      | SignalLogger |               |
    +--------------+--------------+---------------+
    
Additionally, if you need to add a block `foo` to a service without connecting it to any other blocks (e.g. a block which simply serves an HTTP endpoint):

.. code-block:: bash

    $ nio-instance build TestPost 'foo=>'
    +--------------+--------------+---------------+
    | Output Block |      0       |       1       |
    +--------------+--------------+---------------+
    |   CountMe    |     Deb      | TwitterPoster |
    |     met      | SignalLogger |               |
    |   PostToMe   |   CountMe    |               |
    |     Deb      | SignalLogger |               |
    |     foo      |              |               |
    +--------------+--------------+---------------+
    
In this case, `foo` has no receivers, and any that you add will appear starting from column 0 of the execution table.

Voila! You're now up and running with the NIO command line interface. Happy hacking!