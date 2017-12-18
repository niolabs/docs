# Pubkeeper

{% video %}https://www.youtube.com/watch?v=8d3ACNVVhKA{% endvideo %}

Pubkeeper is the nio communications broker. Using standard publish-subscribe patterns, Pubkeeper can orchestrate communications in systems that contain a variety of devices and protocols.

At the root of the Pubkeeper component is the Pubkeeper server. All devices running the Pubkeeper client will register with this Pubkeeper server.

The Pubkeeper server is a matchmaker, not a translator. It is aware that two different devices share a common protocol, but it does not need to understand how that protocol works. The Pubkeeper server is ignorant of a protocol's methods and the contents of any signal, but it intelligently constructs a pathway for two devices to communicate with one another. As a result, signals are able move directly between devices and do not need to be routed through the Pubkeeper server.

Pubkeeper clients can be extremely diverse. Every instance of nio includes the ability to be a Pubkeeper client. Other examples of potential Pubkeeper clients include a website, a Raspberry Pi, a laptop, or a cloud instance. Currently, a Pubkeeper client must be able to communicate to the Pubkeeper server via a websocket.

When you use Publisher or Subscriber blocks within nio, you create Pubkeeper communication channels. A Publisher will create a Pubkeeper “brewer” and a Subscriber will create a Pubkeeper “patron” for the block’s respective topic.

To define which protocols your nio instance supports, you must register Pubkeeper “brews” in your instance configuration. Some common brews available on nio instances include a local brew, a websocket brew, and a ZMQ brew. For communications on the same piece of hardware, the most efficient pub-sub protocol is direct, local communication or a local brew. For communication between different pieces of hardware on the same network, communication using common IoT protocols such MQTT or ZMQ might be the best choice. For communication between networks, websocket is currently the most effective.

## Pubkeeper Security

Pubkeeper simplifies security because Pubkeeper clients encrypt the data before it is published. The encrypted signal is sent over the network and isn’t decrypted until it reaches its final destination. This is known as end-to-end encryption. You can configure your Pubkeeper encryption keys and certificates in your instance’s configuration file.

## How to Use Pubkeeper

### In the Cloud
When you create a system in the System Designer, by default, a Pubkeeper server is spun up in the cloud. You can override this behavior by selecting something other than “auto” in the “advanced” section of the `create system dialog`. You can see the configuration of the cloud Pubkeeper server if you select a system then click the `edit` icon in the contextual toolbar.

{% include "/includes/pubkeeper-config.md" %}

Using Pubkeeper in your running nio instances along with the websocket brew allows you to take advantage of the real-time logging feature of the System Designer. If your nio instance is configured to use the websocket brew and the Pubkeeper connection information in the System Designer, then you can view real-time logs from your instance by clicking the `Open Logger Panel` button. Without Pubkeeper and the websocket brew, you would only be able to view historical logs, not streaming logs.

To see which brews are configured for your project, go to the `[pubkeeper_client]` section of your `nio.conf` file in your project directory.

### Locally
If your nio license includes the Pubkeeper component, you can also run a Pubkeeper server on a local instance. See the documentation at [docs.pubkeeper.com](https://docs.pubkeeper.com) to learn more.
