# Publishing and Subscribing to Data in n.io

Designing systems with n.io means designing how information (i.e., signals) moves throughout the system. The recommended way to get data from one service to another is to use the Pub/Sub mechanisms that are built in to n.io. This can be done using the `Publisher` and `Subscriber` blocks that come in the [communication block repository](https://github.com/nio-blocks/communication). 

## Topic Tree

When using the `Publisher` and `Subscriber` blocks you will need to decide which topic you wish to publish to or subscribe to. The information organization of an entire n.io system can be viewed as a hierarchical topic tree.

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

Subscribers can subscribe to a single topic or also portions of the topic tree through a similar dot-separated string that publishers use. The only difference is that subscribers can supply wildcards represented as `*` and `**`. The single star will match one and only one level of the topic tree. The double star will match zero or more levels of the topic tree. Below are some examples of subscribers and the corresponding publishers they would receive data from according to the publisher examples above.

 * Subscribe: `California.*.Temperature` - Publishers: 1, 3
 * Subscribe: `California.*.Population` - Publishers: 2 - Publisher 4 is not matched because of the use of the single star
 * Subscribe: `California.**.Population` - Publishers: 2, 4 - Publisher 4 is matched this time because we supplied a double star which can match zero levels of the tree.
 * Subscribe: `**.Temperature` - Publishers: 1, 3, 5
 * Subscribe: `California.*.*` - Publishers: 1, 2, 3
 * Subscribe: `California.*.**` - Publishers: 1, 2, 3 - Publisher 4 is still not matched because of the single star which forces us down one more level
 * Subscribe: `California.**` - Publishers: 1, 2, 3, 4

## Pubkeeper

Perhaps the most impactful reason to use the n.io pub/sub system is because of the agnosticism it enables through the use of [Pubkeeper](https://pubkeeper.com). The use of Pubkeeper allows us to separate our information hierarchy (topic tree) from the underlying protocols that will be responsible for transmitting data between services and instances. In other words, it allows service designers to define what data goes to which services without worrying about how it will get there.

## Hints in the System Designer

One of the benefits to using the n.io pub/sub mechanism is that the System Designer understands the topic tree as well. If your service has a `Publisher` or `Subscriber` block with a topic, the designer can show you services that either subscribe to or publish to that topic, respectively. It also allows the System Designer to draw the graph relationship between services and instances.
