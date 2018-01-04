# Build

This final subcommand allows you to build NIO services from the command line by creating links between blocks that are loaded into the sytem. First, let's use `ls` to check out the execution of the `TestPost` service and view the list of blocks available in the system.

```
    $ nio ls services TestPost --exec
    +--------------+--------------+
    | Output Block |      0       |
    +--------------+--------------+
    |     met      | SignalLogger |
    |   CountMe    |     Deb      |
    |     Deb      | SignalLogger |
    |   PostToMe   |   CountMe    |
    +--------------+--------------+

    $ nio ls blocks
    +----------------+--------------+-----------+
    | name           |     type     | log_level |
    +----------------+--------------+-----------+
    | count          |   Counter    |   ERROR   |
    | met            |   Metrics    |   ERROR   |
    | SignalLogger   | Loggger      |   DEBUG   |
    | PostToMe       |  WebHandler  |   DEBUG   |
    | Deb            |  Debounce    |   ERROR   |
    | FacebookPoster | FacebookPost |   ERROR   |
    | CountMe        |   Counter    |   ERROR   |
    | fil            |    Filter    |   ERROR   |
    | TwitterPoster  | TwitterPost  |   DEBUG   |
    +----------------+--------------+-----------+
```
Finally, we can use `build` to connect the outputs of `CountMe` and `PostToMe` to the input of another block!

```
    $ nio build TestPost CountMe TwitterPoster
    +--------------+--------------+---------------+
    | Output Block |      0       |       1       |
    +--------------+--------------+---------------+
    |   CountMe    |     Deb      | TwitterPoster |
    |     met      | SignalLogger |               |
    |   PostToMe   |   CountMe    | TwitterPoster |
    |     Deb      | SignalLogger |               |
    +--------------+--------------+---------------+
```
The build subcommand behaves somewhat similarly to the UNIX `cp` command in that it takes a series of *n* block instances of which the firs *n-1* represent "source" blocks, while the *n* th block is the single sink.
Additionally, if you need to add a block `fil` to a service without connecting it to any other blocks (e.g. a block which simply serves an HTTP endpoint):

```
    $ nio build TestPost fil
    +--------------+--------------+---------------+
    | Output Block |      0       |       1       |
    +--------------+--------------+---------------+
    |   CountMe    |     Deb      | TwitterPoster |
    |     met      | SignalLogger |               |
    |   PostToMe   |   CountMe    |               |
    |     Deb      | SignalLogger | TwitterPoster |
    |     fil      |              |               |
    +--------------+--------------+---------------+
```
In this case, `fil` has no receivers, and any that you add will appear starting from column 0 of the execution table.
Finally, if you'd like to remove blocks/block connections instead of create them, just append the `-rm` option to any of the above `build` invocations.


--------
The `build` command (Doesn't really do anything as of now)
