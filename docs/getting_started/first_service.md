# Building Your First {{ book.product }} Service

In the System Designer, you begin with an empty canvas full of possibilities, but there are no services yet. While it won't get too exciting quite yet, you can start by building a very basic service to simulate and log signals.

To add a service:

1. Select the name of the instance.
2. Click **Add New Service**. 
3. Type **SimulateAndLog**, leave the service type as **Service**, and click **Accept**.
4. Select the **SimulateAndLog** service.
5. In the Search box, type `counterintervalsimulator`.
6. Click  **Install Block**.
7. Drag the **CounterIntervalSimulator** block on to the canvas.
8. Name the block **Simulate** and click **Accept**.
9. Double-click the **Simulate** block to open the properties and click **Save**.
5. In the Search box, type `logger`. 
6. Click **Install Block**.
5. Drag the **Logger** block onto the canvas.
6. Name the block **Log** and click **Accept**.
9. Double-click the **Log** block to open the properties and click **Save**.
9. Click and drag the output terminal of the **Simulate** block and release it on the input terminal of the **Log** block to connect the blocks.
10. Click **Save**.

## Run Services

By now, you are more than ready to see something happen.

1. Click **Start** on the toolbar.
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
3. Click **Stop** when finished.

## Configure Blocks

So far you have only viewed the default behavior of this block. You can configure the Simulate block to change the interval from 1 to 2 seconds to see the signals logged every other second.

To configure blocks:
1. Double-click the **Simulate** block to view the properties in the dialog box.
2. Change the interval value from **1** \(the default\) to **2**.
3. Click **Save**.

## Command Blocks and Services

You can execute code in a block or service with commands. Technically, you have already commanded services with start and stop. 

To command a block:

1. With SimulateAndLog running, select the **Log** block.
2. Click **Command** **(&lt;/&gt;)** on the toolbar.
3. In the Command block dialog, type in a phrase in the results box.
4. Click **Execute** to view the phrase logged with the simulate signals.

## Conclusion

At this point you should feel comfortable installing {{ book.product }}, creating a project with blocks, and configuring and running services. You can find block documentation on the [nio-blocks repository](https://github.com/nio-blocks).
   
