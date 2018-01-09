# Add Instance

Once you have a local instance running, you can edit it using the nio System Designer. The log messages indicate that your nio instance is available at `http://localhost:8181`. Based on the configured **access mode** in the instance, you need Basic Authentication to communicate with the instance. To connect to your local instance:

1. Select the name of your nio system, either in the left navigation panel or the breadcrumb above the contextual toolbar.
1. Click **create local instance**.
1. Complete the **create local instance** window:
  * In the **instance name** box, enter your instance name.
  * In the **hostname** box, enter **localhost**.
  * In the **port** box, enter **8181**.
  * Leave the **access mode** as **basic**.
1. Click **accept**.

> Note: When the System Designer connects to a nio instance, it communicates with that instance directly from your browser via an XHR request. Hostnames like `localhost` and other internal IP addresses will work. You must have access to the localhost or other IP address from your machine to use the System Designer.

You may see an issue regarding HTTPS and HTTP instances. Since you launched your instance and presumably didn't load any SSL certificates, the instance is accessible only by HTTP. However, if you are logged into the System Designer via HTTPS, your browser will restrict an XHR request going over HTTP. To connect to a local instance, you can log into the designer via HTTP at http://designer.n.io. All of your instances and systems will be the same, except the nio commands to edit these instances won't happen over HTTPS.

Once your instance is loaded and available, you can add services and blocks in the same manner as the [cloud instance](../in-the-cloud.md#create-service).

Available nio Blocks can be explored in the nio [Block Library](https://blocks.n.io) where you will find a summary of the block's purpose, a list of its properties, commands, inputs, and outputs, and a link to the block code repository.
