# Simulators

Most of the time, the first service you build with the nio Platform involves simulating signals using a _Simulator_ block and then logging that data using a _Logger_ block. That is the "Hello, World" nio service. However, simulators are much more powerful and do much more than generate random data. This document attempts to define and explain other use cases for simulators.

## Understanding Simulators

Before we get into too many use cases, it is helpful to understand how simulators work along with their naming conventions. There are many types of simulator blocks, but once you understand the naming, their function will be clear. The basic idea is that a simulator block consists of a generator and a trigger. Each simulator block will be named `<Generator><Trigger>Simulator`. For example, if you want to use the `Counter` generator and the `Interval` trigger as your simulator, then you can use the _CounterIntervalSimulator_ block type.

### Generators

Generators define the shape and contents of the signals that are emitted.

* `Counter`—Each new signal generated will have an attribute that is incremented by some value.
* `File`—Each new signal generated is pulled from a file of signals.
* `Identity`—Each signal generated is an empty signal `{}`.

### Triggers

Triggers define when a simulator should notify signals. Triggers  are only concerned with the timing of simulators.
* `Interval` - Notify signals at a fixed time interval \(for example, every 5 minutes\)
* `Cron` - Notify signals at certain times of the day, similar to how you would configure a [cron job](https://en.wikipedia.org/wiki/Cron)

## Driving Another Block

The general design of nio assumes that **signals** represent data and information, while **blocks** represent functions and transformations. However, blocks need to know when and how to perform these functions. Some blocks may need to do an action periodically while others may need to wait for some external action, such as a button press. To avoid building that logic in the block's configuration, you can use incoming signals to trigger the action instead. This also allows the block to "tap in to" the incoming signals and perhaps change its behavior based on the content of the signals. For example, rather than making a fixed HTTP request every interval, a block could send the contents of the incoming signal as part of the HTTP payload instead.

In some cases, you will not care about the contents of the incoming signal, but you will want to perform an action. For example, if you wanted to poll the Twitter API every five minutes for new tweets, you would need an incoming signal to the Twitter block when you wanted to poll. Since you don't care about the contents of the signal, any signal, even an empty signal, would suffice. You could use the _IdentityIntervalSimulator_ to create the signal and kick-off polling of the Twitter block. The Identity generator combined with the Interval trigger would drive the block to periodically poll the API.

Because of the way we use simulators to kick off the actions of a service, almost every service will either begin with a _Subscriber_ block \(to subscribe to signals from another service\) or with a _Simulator_ block \(to generate the driving signals on its own\).

## Testing and Custom Simulators

To test a service, you may want data that looks like an actual signal without connecting to a real data source. To do this, you can create a custom generator for your data format and then use a simulator block with that generator. The process of creating a custom generator requires writing python code and is documented in more detail in the [signal generator/simulator](https://blocks.n.io/?category=Signal%20Generator) README files on GitHub.

You can create custom simulated data without writing any code, but this is not as flexible. By pairing a simulator with the `Identity` trigger and a _Modifier_ block, a service builder can generate empty signals on a schedule and then route the empty signal to a _Modifier_ block where it fills in the information that the signal should consist of. A service building expert would make use of the `random` module inside of a nio expression to generate random data. For example, to generate a signal with a random number from 1 to 10 each time, connect the output of an _IdentityIntervalSimulator_ block to a _Modifier_ block.
```
{
  "name": "Random Number",
  "type": "Modifier",
  "fields": [{
    "title": "num",
    "formula": "{{ random.randint(1,10) }}"
  }]
}
```
