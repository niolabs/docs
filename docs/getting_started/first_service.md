# Building Your First {{ book.product }} Service

In the System designer, you start with an empty canvas full of possibilities, but there are no services yet. We will add a service to fix that. While it won't get too exciting quite yet, we can start by building a very basic service to simulate and log signals.

To add a service:

1. Select the name of the instance you created.
2. Click "Add New Service."
3. Type SimulateAndLog, leave the service type as Service, and click "Accept."
4. Double-click on the SimulateAndLog Service.
5. From the right, click on "LB" and drag a LoggerBlock block on to the canvas.
6. Name the block Log.
7. Click on CIS and drag a CounterIntervalSimulator block on to the canvas.
8. Name the block Simulate.
9. Connect the blocks by clicking and dragging the output terminal of the Simulate block and release it on the input terminal of the Log block.
10. Click Save.

## Running Services

By now, you are more than ready to see something happen.

1. Click the "start" icon from the top of the service canvas.
2. View the logs in the terminal.  Note: Logs are saved in the  `logs/` directory of your project folder.

```
[2016-03-05 00:32:05.189] NIO [INFO] [SimulateAndLog.Log] Block : Log (type : LoggerBlock) status is configured
[2016-03-05 00:32:05.189] NIO [INFO] [SimulateAndLog.Log] Block: Log (type: LoggerBlock) status is configured
[2016-03-05 00:32:05.191] NIO [INFO] [SimulateAndLog.service] Service: SimulateAndLog status changed from: configuring to: configured
[2016-03-05 00:32:05.193] NIO [INFO] [SimulateAndLog.service] Service: SimulateAndLog status changed from: configured to: starting
[2016-03-05 00:32:05.199] NIO [INFO] [SimulateAndLog.Log] Block: Log (type: LoggerBlock) status is starting
[2016-03-05 00:32:05.199] NIO [INFO] [SimulateAndLog.Log] Block: Log (type: LoggerBlock) status is started
[2016-03-05 00:32:05.200] NIO [INFO] [SimulateAndLog.service] Service: SimulateAndLog status changed from: starting to: started
[2016-03-05 00:32:05.200] NIO [INFO] [SimulateAndLog.Log] {'sim': 0}
[2016-03-05 00:32:05.201] NIO [INFO] [main.ServiceManager] Service: SimulateAndLog with process identifier(pid): 65638 has started
[2016-03-05 00:32:06.203] NIO [INFO] [SimulateAndLog.Log] {'sim': 1}
[2016-03-05 00:32:07.204] NIO [INFO] [SimulateAndLog.Log] {'sim': 0}
[2016-03-05 00:32:08.204] NIO [INFO] [SimulateAndLog.Log] {'sim': 1}
[2016-03-05 00:32:09.203] NIO [INFO] [SimulateAndLog.Log] {'sim': 0}
[2016-03-05 00:32:10.204] NIO [INFO] [SimulateAndLog.Log] {'sim': 1}
```

3. Click the "stop" icon when finished.

## Configuring Blocks

So far we're only using the default behavior of these blocks, but let's change things up by configuring the Simulate block. We want to change the interval from 1 to 2 seconds to see the signals logged every other second.

To configure blocks:

1. Double-click on the Simulate block to view the properties in a dialog box.
2. Change the interval value from 1 \(the default\) to 2.
3. Click Save.

## Commanding Blocks and Services

Commands are a way to execute code in a block or service. Technically, you've already commanded services with "start" and "stop".

To command a block:

1. With the SimulateAndLog running, select the Log block.
2. Click Command &lt;/&gt; on the menu.
3. Select the Log block and type in a phrase in the results box.
4. Click Execute to view the phrase logged with the simulate signals.

## Conclusion

At this point you should feel comfortable installing {{ book.product }}, creating a project with blocks, and configuring and running services. You can find block [documentation on GitHub](https://github.com/nio-blocks).
