# How to Build a UI for a nio System
The easiest way to create a nio-powered UI is to start with our [UI Scaffold](https://github.com/niolabs/ui-scaffold). It gets you up and running in minutes.

## What’s In The Box
The UI Scaffold:
- Imports ReactJS
- Imports the nio UI Kit component library
- Imports the Pubkeeper browser client
- Imports the Auth0 library to handle authorization (optional)
- Bootstraps a simple site that, when configured, publishes and subscribes to data via your cloud Pubkeeper server

If you’re at all familiar with React, this simple example covers most of what you need to know to get started.

## Hello World (What Time Is It?)
Follow these steps to create a simple UI that can publish to, subscribe to, and display the output of your nio services.
1. In your terminal, clone the UI Scaffold, enter the directory, and install dependencies.
```
git clone https://github.com/niolabs/ui-scaffold.git
cd ui-scaffold
npm i -s
```
2. In the root of the project, update the `config.js` file.
  1. Open the System Designer in a browser: https://designer.n.io/.
  2. Select your system in the left-hand navigation.
      1. If you need to create your first system, follow the instructions [here](/system-designer/designer-tasks.html).
  2. Click the **edit** button in the contextual toolbar to open its configuration.
  2. Copy the values for `hostname` and `token` into the `config.js` file.
  2. Use the Pubkeeper hostname as your `WS_HOST`, replacing the word “pubkeeper” with “websocket”.
      1. For example, if your Pubkeeper hostname was `aaaaa.pubkeeper.nio.works`, your websocket hostname would be `aaaaa.websocket.nio.works`.
1. Start the project.
```
npm start
```
1. Visit the project at https://0.0.0.0:3000.
  1. The development web server uses a self-signed certificate, and you may see a warning about the site being insecure. In your local development environment, it is safe to click “proceed to site anyway."

You’ll see a simple UI with a clock that updates every second.

What’s actually happening is this:
  - The UI connects to your cloud Pubkeeper server.
  - When the main page renders, it sets a local variable of the current time and sets an interval to update that time every second.
  - The Pubkeeper brewer publishes the time to the topic “ui_scaffold.example_brew”.
  - The Pubkeeper patron subscribes to “ui_scaffold.example_brew” topic, receives the data, and delivers it to the handler `writeDataToOutput`, which sets the local state variable `time` equal to the inbound time.
  - The React `Clock` component from the nio UI Kit then renders itself based on the inbound time.

Sure, you could have just had the timer set the local state variable, but then you wouldn’t have become such an expert at using Pubkeeper.

## What’s Next?
The output of any service that shares the same Pubkeeper host and token that you configured above can be consumed by your UI. All you need to do is update the patron’s topic (or add new patrons!), register a handler, and render the data.
The nio UI Kit at [https://uikit.niolabs.com](https://uikit.niolabs.com) is full of components for layout, charts, etc. that can be pulled into any React project that accommodates scss (we use webpack).

Of course, if React isn’t your thing, the Pubkeeper browser client can be used on any site that supports JavaScript:
 ```
 npm i -s @pubkeeper/browser-client
 ```
