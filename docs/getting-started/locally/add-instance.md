# Add Instance

Once you have a local instance running, you can edit it using the System Designer. The log messages indicate that your nio instance is available at `http://localhost:8181` and you need basic authentication to communicate with the instance. To connect to your local instance:

1. Select the name of your system, either in the left navigation panel or the breadcrumb above the contextual toolbar.
1. Click **create local instance**.
1. Complete the **create local instance** window:
  * In the **instance name** box, enter your instance name.
  * In the **hostname** box, enter **localhost**.
  * In the **port** box, enter **8181**.
  * Leave the **access mode** as **basic**.
1. Click **accept**.
1. Wait for the instance to spin-up and note the name of the new instance on the left.

> Note: When the System Designer connects to a nio instance, it communicates with that instance directly from your browser via an XHR request. Hostnames like `localhost` and other internal IP addresses will work. You must have access to the localhost or other IP address from your machine to use the System Designer.

You may see an issue regarding HTTPS and HTTP instances. Since you launched your instance and presumably didn't load any SSL certificates, the instance is accessible only by HTTP. However, if you are logged into the System Designer via HTTPS, your browser will restrict an XHR request going over HTTP. To connect to a local instance, you can log into the designer via HTTP at http://designer.n.io. All of your instances and systems will be the same, except the nio commands to edit these instances won't happen over HTTPS.

Once your instance is loaded and available, you can add services and blocks in the same manner as the [cloud instance](/getting-started/in-the-cloud#create-a-service).

Available blocks can be explored in the [block library](blocks.n.io) where you will find a summary of the block's purpose, a list of its properties, commands, inputs, and outputs, and a link to the block code repository.

## Create a Service

1. Select the name of your instance under the system name in the left navigation panel or in the breadcrumb above the contextual toolbar.
1. Click **create new service**.
1. Complete the **create new service** window:
  1. In the **service name** box, enter a service name.
  1. Leave the **service type** as **Service**.
1. Click **accept**.
1. Click **save** in the toolbar.
1. Click **auto-start off** in the toolbar.

## Add Blocks
Once you have successfully created a service, you will be switched to the service context where you will see the block library containing blocks available for you to use to build your logic.

### To Add a Block in the System Designer
1. In the **block library** search box, enter a search term. As you type, the list is filtered.
* If the block is not displayed, click **available**, **installed**, and **configured** to search for the block.
* If the block is not already pre-installed, click the **install block** button which resembles a cloud with a down arrow.
1. Drag the block type to the canvas.
1. Name the block.
1. Click **accept**.
