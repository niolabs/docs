# Monitoring Streams
When consuming a stream of signals, it's possible that the source of those signals may malfunction, become unreachable, or otherwise stop supplying valid signals. This condition, a *timeout*, often requires action such as alerts or alternative logic, and for this purpose [_SignalTimeout_](https://blocks.n.io/SignalTimeout) blocks can be used to generate new signals when input signals have stopped.

---

For every signal processed, the _SignalTimeout_ resets an internal timer for every configured **Interval**, which if allowed to expire will emit the last signal received, with a `timeout` attribute added to it. If the incoming signal already has a `timeout` attribute, it will be overwritten with this new value. As long as signals are received at least as often as the configured interval(s), no signals are emitted.

For example, 1 minute after the `important_data` stream stops (perhaps the publisher has stopped, or a network error has ocurred) a signal will be published to `alerts`, and then repeat every minute until the stream is restored. While `important_data` is working normally, no signals are published to `alerts`.
```
+----------------------------------+
| Subscriber                       |
|   Topic: important_data          |
|                                  |
|                                  |
+-----------------O----------------+
                  |
                  |
                  V
+-----------------O----------------+
| SignalTimeout                    |
|   Intervals:                     |
|     Minutes: 1                   |
|     Repeatable: True             |
+-----------------O----------------+
                  |
                  |
                  V
+-----------------O----------------+
| Publisher                        |
|   Topic: alerts                  |
|                                  |
|                                  |
+----------------------------------+
```
Every signal emitted from a _SignalTimeout_ has a new attribute, `timeout`, added to it, which contains a `datetime.timedelta` object. The value of this object is equal to the configured **Interval**, and does not increment if configured **Repeatable**. That is to say, the `timeout` attribute represents the configured **Interval** that was triggered, not the cumulative time elapsed.

In this example we will use a [_StateChange_](https://blocks.n.io/StateChange) to evaluate if a stream is dry or not, and build an alert message based on that. We will also use [signal grouping](https://docs.n.io/service-design-patterns/group_by.html) to monitor multiple streams identified by the value of an `id` attribute. The defined **State** for each **Group** is the value of the incoming signals' `timeout` attribute, which is `False` if the signal was emitted by the subscriber into the _Modifier_. Any value of `timeout` that isn't explicitly `False`, such as a `datetime.timedelta` assigned by the _SignalTimeout_, will be evaluated as `True` and provide a change of state. This [Truth Value Test](https://docs.python.org/3/library/stdtypes.html#truth-value-testing) is also used in the [_ConditionalModifier_](https://blocks.n.io/ConditionalModifier)  to determine which `message` to build. In this configuration a single, customized alert can be sent when a stream goes dry, and another distinct message when it resumes.
```
                     +----------------------------------+
                     | Subscriber                       |
                     |   Topic: important_data          |
                     |                                  |
                     |                                  |
                     +----------------O-----------------+
                                      |
                  +-------------------+--------------------+
                  |                                        |
                  V                                        V
+-----------------O----------------+     +-----------------O----------------+
| Modifier                         |     | SignalTimeout                    |
|   Fields:                        |     |   Group By: {{ $id }}            |
|     Attribute Name: timeout      |     |   Intervals:                     |
|     Attribute Value: {{ False }} |     |     Seconds: 10                  |
+-----------------O----------------+     +-----------------O----------------+
                  |                                        |
                  |                                        |
                  +-------------------+--------------------+
                                      |
                                      |
                                      V
                     +----------------O-----------------+
                     | StateChange                      |
                     |   Group By: {{ $id }}            |
                     |   State: {{ $timeout }}          |
                     |                                  |
                     +----------------O-----------------+
                                      |
                                      |
                                      V
                +---------------------O----------------------+
                | ConditionalModifier                        |
                |   Fields:                                  |
                |     Attribute Name: message                |
                |     Lookup:                                |
                |       Formula: {{ $state }}                |
                |       Attribute Value: Alert! {{ $group }} |
                |                                            |
                |       Formula: {{ not $state }}            |
                |       Attribute Value": {{ $group }} OK    |
                +---------------------O----------------------+
```
## The More You Know:
A `datetime.timedelta` object is represented as three integers in the service logs, such as `{timeout: datetime.timedelta(<days>, <seconds>, <microseconds>)}`, and can be easily converted into seconds: `{{ $timeout.total_seconds() }}`. For more information see the [Python Standard Library](https://docs.python.org/3/library/datetime.html#timedelta-objects).
