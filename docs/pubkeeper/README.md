# <span class="allow-caps">Pubkeeper</span>

Pubkeeper is the nio Platform communications broker. Using standard publish-subscribe patterns, Pubkeeper can orchestrate communications in systems that contain a variety of devices and protocols.

&nbsp;

{% video %}https://www.youtube.com/watch?v=8d3ACNVVhKA{% endvideo %}

---
## <span class="allow-caps">Pubkeeper</span> server

At the root of the Pubkeeper component is the Pubkeeper server. All devices running the Pubkeeper client will register with this Pubkeeper server.

The Pubkeeper server is a matchmaker, not a translator. It is aware that two different devices share a common protocol, but it does not need to understand how that protocol works. The Pubkeeper server is ignorant of a protocol's methods and the contents of any signal, but it intelligently constructs a pathway for two devices to communicate with one another. As a result, signals are able move directly between devices and do not need to be routed through the Pubkeeper server.

---
## <span class="allow-caps">Pubkeeper</span> clients

Pubkeeper clients can be extremely diverse. Every instance of nio includes the ability to be a Pubkeeper client. Other examples of potential Pubkeeper clients include a browser, a Raspberry Pi, a laptop, or a cloud instance. Currently, a Pubkeeper client must be able to communicate to the Pubkeeper server via a websocket.

When you use _Publisher_ or _Subscriber_ blocks within nio, you create Pubkeeper communication channels. A _Publisher_ will create a Pubkeeper “brewer” and a _Subscriber_ will create a Pubkeeper “patron” for the block’s respective topic.

To define which protocols your nio instance supports, you must register Pubkeeper “brews” in your instance configuration. Some common brews available on nio instances include:

 * **local**<br/>
 For communications on the same piece of hardware, the most efficient pub-sub protocol is direct, local communication or a local brew.

 * **websocket**<br />
 For communication between networks, websocket is currently the most effective.

 * **ZMQ / MQTT**<br />
 For communication between different pieces of hardware on the same network, communication using common IoT protocols such MQTT or ZMQ might be the best choice.


---
## Security

Pubkeeper simplifies security because Pubkeeper clients encrypt the data before it is published. The encrypted signal is sent over the network and isn’t decrypted until it reaches its final destination. This is known as end-to-end encryption. You can configure your Pubkeeper encryption keys and certificates in your instance’s configuration file.

---
## Use nio-managed cloud <span class="allow-caps">Pubkeeper</span>

<img class="right border" src="/img/pubkeeper-edit-modal.png" width="250" />

When you create a system in the nio System Designer, by default, a Pubkeeper server is spun up in the cloud. You can override this behavior by selecting something other than “auto” in the “advanced” section of the **create system** dialog. You can see the configuration of the cloud Pubkeeper server if you select a system then click the **edit** icon in the contextual toolbar.

To configure your local project to use the cloud Pubkeeper server, copy the Pubkeeper `host`, `port`, `token`, and `secure` settings shown in your system's edit modal to the following four lines in the `# Pubkeeper Client` section of your project directory's `nio.conf` file under the `[user_defined]` section:

  ```
  # Pubkeeper Client
  PK_HOST=[your copied host]
  PK_PORT=443
  PK_TOKEN=[your copied token]
  PK_SECURE=True
  ```

Alongside your system’s Pubkepeer server, a websocket server is also spun up that can be used by websocket brews. To use this websocket brew in your local nio instance, update the following three lines in the `# WebsocketBrew Variables` of your project directory's `nio.conf` file under the `[user_defined]` section:

  ```
  # WebsocketBrew Variables
  WS_HOST=[your copied host, replacing `pubkeeper` with `websocket`]
  WS_PORT=443
  WS_SECURE=True
  ```

Using Pubkeeper in your running nio instances along with the websocket brew allows you to take advantage of the real-time logging feature of the System Designer. If your nio instance is configured to use the websocket brew and the Pubkeeper connection information in the System Designer, then you can view real-time logs from your instance by clicking the **open logger panel** button. Without Pubkeeper and the websocket brew, you would only be able to view historical logs, not streaming logs.

To see which brews are configured for your project, go to the `[pubkeeper_client]` section of your `nio.conf` file in your project directory.

---
## Use <span class="allow-caps">Pubkeeper</span> locally

If your nio license includes the Pubkeeper component, you can also run a Pubkeeper server on a local instance. See the documentation at [docs.pubkeeper.com](https://docs.pubkeeper.com) to learn more.

---
## Documentation

Find the documentation for Pubkeeper at [docs.pubkeeper.com](https://docs.pubkeeper.com).
