# Publishing and Subscribing to Data

An easy way to communicate between nio services and instances in the nio Platform is by using a publisher/subscriber pattern.

The following communication blocks are used for publishing and subscribing to data signals:
* [_Publisher_](https://blocks.n.io/Publisher)
* [_Subscriber_](https://blocks.n.io/Subscriber)

---

## Topic Tree

When using the _Publisher_ and _Subscriber_ blocks, you connect systems and instances by defining a topic you wish to publish to or subscribe to. The information structure of an entire nio system can be viewed as a hierarchical topic tree.

### Publishers

Publishers publish data to a specific topic, denoted by a dot-separated string. The following is an example of publisher topics and the resulting topic tree that would be generated in the system.

Publisher Topics:

1. California.San Francisco.Temperature
2. California.San Francisco.Population
3. California.Los Angeles.Temperature
4. California.Population
5. Colorado.Broomfield.Temperature

These topics can be visualized as the following tree:

```
                                        ┌────────┐
                                        │  Root  │
                                        └────────┘
                                             │
                            ┌────────────────┴──────────────────┐
                            ▼                                   ▼
                     ┌────────────┐                      ┌────────────┐
                     │ California │                      │  Colorado  │
                     └────────────┘                      └────────────┘
                            │                                   │
              ┌─────────────┴──────┬─────────────┐              │
              ▼                    ▼             ▼              ▼
       ┌────────────┐       ┌────────────┐┌────────────┐ ┌────────────┐
       │    San     │       │    Los     ││    (4)     │ │ Broomfield │
       │ Francisco  │       │  Angeles   ││ Population │ │            │
       └────────────┘       └────────────┘└────────────┘ └────────────┘
              │                    │                            │
       ┌──────┴──────┐             │                            │
       ▼             ▼             ▼                            ▼
┌─────────────┬────────────┐┌─────────────┐              ┌─────────────┐
│     (1)     │    (2)     ││     (3)     │              │     (5)     │
│ Temperature │ Population ││ Temperature │              │ Temperature │
└─────────────┴────────────┘└─────────────┘              └─────────────┘
```

### Subscribers

Subscribers can subscribe to a single topic or also portions of the topic tree through a similar dot-separated string that publishers use. The only difference is that subscribers can supply wildcards represented as `*` and `**`. The single asterisk will match one and only one level of the topic tree. The double asterisk will match zero or more levels of the topic tree. Below are some examples of subscribers and the corresponding publishers they would receive data from according to the publisher examples above.

* Subscribe: `California.*.Temperature`—Publishers: 1, 3
* Subscribe: `California.*.Population`—Publishers: 2 (Publisher 4 is not matched since the single asterisk is used.)
* Subscribe: `California.**.Population`—Publishers: 2, 4 (Publisher 4 is matched this time because we supplied a double asterisk which can match zero levels of the tree.)
* Subscribe: `**.Temperature`—Publishers: 1, 3, 5
* Subscribe: `California.*.*`—Publishers: 1, 2, 3
* Subscribe: `California.*.**`—Publishers: 1, 2, 3 (Publisher 4 is still not matched since the single asterisk forces us down one more level)
* Subscribe: `California.**`—Publishers: 1, 2, 3, 4

---

## Pubkeeper

Perhaps the most impactful reason to use the nio pub/sub system is because of the interoperability enabled through the use of [Pubkeeper](/pubkeeper/README.md). Pubkeeper allows the information hierarchy, or topic tree, to be independent of the underlying protocols that are be responsible for transmitting data between services and instances. In other words, it allows service designers to define what data goes to which services without worrying about how it will get there.

---

## Hints in the System Designer

Another benefit of using the nio pub/sub mechanism is that the nio System Designer understands the topic tree as well. If your service has a _Publisher_ or _Subscriber_ block with a topic, the designer can show you services that either subscribe to or publish to that topic, respectively. It also permits the System Designer to draw the graph relationship between services and instances that share topics.
