# How to build a UI for a nio system
The easiest way to create a nio Platform-powered UI is to start with our [UI scaffold](https://github.com/niolabs/ui-scaffold). It gets you up and running in minutes.

---

## What’s in the box

- **From niolabs**
    - [niolabs ui-kit](https://uikit.niolabs.com/) for components and styles
    - [niolabs Pubkeeper](https://niolabs.com/product/pubkeeper) for publishing and subscribing to topics


- **Third party software** (click to review each library's licensing)
    - [ReactJS](https://reactjs.org/) site scaffold
    - [react-router](https://reacttraining.com/react-router/) for navigation
    - [webpack 3](https://webpack.js.org/) module bundling and development webserver
    - [auth0](https://auth0.com/) for securing the site (optional, default true)


If you are at all familiar with React, this simple example covers most of what you need to know to get started.

---

## Hello world (what time is it?)

Follow these steps to create a simple UI that can publish to, subscribe to, and display the output of your nio services.

1. In your terminal, clone the UI scaffold, enter the directory, and install dependencies.
    ```
    git clone https://github.com/niolabs/ui-scaffold.git my-project
    cd my-project
    npm i -s
    ```
1. In the root of the project, rename **config.js.example** to `config.js`, and open it in a text editor.
    1. **Never commit configuration details! We've added `config.js` to `.gitignore`. Even though these are public urls and tokens, it's bad practice to commit them. For deployment, make sure you put `config.js` at your project root.**
1. Get your Pubkeeper **hostname** and **token** from your nio-managed cloud-instance:
    1. Open the nio **System Designer** in a browser: https://designer.n.io/.
    1. Select your system in the left-hand navigation.
        1. If you need to create your first system, follow the instructions [here](/system-designer/designer-tasks.html).
    1. Click the **edit** button in the contextual toolbar to open its configuration.
1. In `config.js`:
    1. Set `PK_HOST` to your **hostname** value.
    1. Set `PK_JWT` to your **token** value.
    1. Set `WS_HOST` to your **hostname** value, but swap the word 'pubkeeper' for 'websocket' (e.g., if your **hostname** is `aaaaa.pubkeeper.nio.works`, use `aaaaa.websocket.nio.works`).
1. Start the project.
    ```
    npm start
    ```
1. Visit the project at https://0.0.0.0:3000.
    1. The development web server uses a self-signed certificate, and you may see a warning about the site being insecure. In your local development environment, it is safe to click "Advanced" > "proceed to site anyway."

You will see a simple UI with a clock that updates every second.

### What’s actually happening?

  - The UI connects to your cloud Pubkeeper server.
  - When the main page renders, it sets a local variable of the current time and sets an interval to update that time every second.
  - The Pubkeeper brewer publishes the time to the topic **ui_scaffold.example_brew**.
  - The Pubkeeper patron subscribes to **ui_scaffold.example_brew** topic, receives the data, and delivers it to the handler `writeDataToOutput`, which sets the local state variable `time` equal to the inbound time.
  - The React `Clock` component from the nio UI Kit then renders itself based on the inbound time.

Sure, you could have just had the timer set the local state variable, but then you wouldn’t have become such an expert at using Pubkeeper.

---

## What’s next?
The output of any service that shares the same Pubkeeper host and token that you configured above can be consumed by your UI. All you need to do is update the patron’s topic (or add new patrons!), register a handler, and render the data.
The nio UI Kit at [https://uikit.niolabs.com](https://uikit.niolabs.com) is full of components for layout, charts, etc. that can be pulled into any React project that accommodates scss (we use webpack).

Of course, if React isn’t your thing, the Pubkeeper browser client can be used on any site that supports JavaScript:
 ```
 npm i -s @pubkeeper/browser-client
 ```

---

### Apache 2.0 License

Copyright 2017-2018 n.io innovation, LLC

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
