![Pubkeeper config](/img/pubkeeper-edit-modal.png)

To configure your local project to use the cloud Pubkeeper server, copy the Pubkeeper 'host', 'port', 'token', and 'secure' settings shown in your system's edit modal to the following four lines in the `# Pubkeeper Client` section of your project directory's `nio.env` file:

  ```
  PK_HOST: [your copied host]
  PK_PORT: 443
  PK_TOKEN: [your copied token]
  PK_SECURE: True
  ```

Alongside your system’s Pubkepeer server, a websocket server is also spun up that can be used by websocket brews. To use this websocket brew in your local nio instance, update the following three lines in the `# WebsocketBrew Variables` section:

  ```
  WS_HOST: [your copied host, replacing `pubkeeper` with `websocket`]
  WS_PORT: 443
  WS_SECURE: True
  ```
