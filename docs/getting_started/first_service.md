# Building Your First n.io Service

In the System designer, you start with an empty canvas full of possibilities, but there are no services yet. We will add a service to fix that. While it won't get too exciting quite yet, we can start by building a very basic service to simulate and log signals.

By default, the projects logs go to standard out as well as to files in the `logs/` directory of your project folder.



To add a block:

1. Click "All" on the right side of the screen. If you have an empty instance, no blocks will be displayed.
2. Click the Add Block icon which looks like a cloud with an arrow.
3. To import the block, enter the Github clone URL of the block, and click "Accept."
4. After uploading, the block type displays on the right side of the screen under its group.

Start by clicking the "add new service" button and name your service "SimulateAndLog".

Now that we have a service, we'll add a CounterIntervalSimulator block and a Logger block. Double click on your "SimulateAndLog" service. From the right, click on "LB" and drag a LoggerBlock onto the service canvas. Go ahead give it the name "Log". Do the same with "CIS" and drag in a CounterIntervalSimulator and name it "Simulate".

Now connect these blocks by clicking and dragging on the output terminal of "Simulate" and release it on the input terminal of "Log".

Once you are satisfied with your service, click the "save" icon at the top of the instance canvas.

## Running Services

By now I'm sure you're more than ready to see something happen. Click the "start" icon from the top of the service canvas and you should see some logs appear in the terminal where you ran n.io from.

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

Click the "stop" icon when you're ready to move on.

## Configuring Blocks

So far we're only using the default behavior of these blocks. Why don't you try changing things up by configuring the Simulate block. Click on the top right of the block and take a look at it's properties on the pop out menu. You'll notice that Interval is configured to 1 second. Change that to 2 and then click "save". Now when you start the service, you'll only see signals logged every other second.

## Commanding Blocks and Services

Commands are a way to execute code in a block or service. Technically, you've already commanded services with "start" and "stop".

Running blocks can also be commanded. With the SimulateAndLog service running, select the Log block and then click the "command" button from the menu. Select "log", type in a phrase and then click "execute". You'll see your phrase logged alongside the simulated signals.

## Conclusion

At this point you should feel comfortable installing n.io, creating a project with blocks, and configuring and running services. You can find block [documentation on GitHub](https://github.com/nio-blocks).

