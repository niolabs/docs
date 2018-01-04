# Command

This subcommand allows you to send commands to live instances. Because of the way blocks are referenced within NIO, you must supply the target command, the name of the service, and (if you are commanding a block) the name of the block instance.
.. code-block:: bash
    $ nio co start TestPost
    `http://localhost:8181/services/TestPost//start` was processed successfully

The syntax for adding parameters to commands is as follows:
.. code-block:: bash

    $ nio co log TestPost SignalLogger --args 'phrase=foobar'

Passing the `--auto` (`-a`) flag to command tells **nio** to read command arguments from the command line.

If the command response body is non-empty, its contents are printed to stdout; otherwise, the terminal remains silent.
