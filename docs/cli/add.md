# Add Block

This subcommand adds new block types to and existing nio project. By defualt they are pulled from the official [nio GitHub](https://github.com/nio-blocks) account.
This must be run from the root level of the project that you want to add the blocks too. One ore morse lists can be added at a time.
.. code-block:: bash
    $ nio add logger
    $ ls blocks
    logger
    $ nio add counter simulator
    $ ls blocks
    counter logger simulator
