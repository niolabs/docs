# Running n.io in the Cloud

The easiest way to get n.io up and running is to launch a cloud instance of n.io. To do that, log in to the [System Designer](https://designer.n.io) and select a system to add an instance to on the left side. If you do not have any systems yet, create one by clicking the "+" icon on the left bar.

Once a system is selected \(you can tell by the breadcrumb at the top of the system designer only showing the system name\), you can add a cloud instance to it by clicking "Create a Cloud Instance."

Give your instance a name and select "n.io Cloud" as the instance type. The instance should appear on the left navigation of your system. It may take some time for the instance to fully spin up. Once the instance is completely launched, select it from the instance list on the left. You can tell the instance is selected by the breadcrumb \(should show all the way to the instance level\) and by the up arrow icon on the instance list to the left.

## Add a Service and Blocks

You have an instance but it is empty, let's fix that! Select your instance and then click the "Add New Service" button at the top. Give your service a name and leave the service type as "Service." The service should auto select itself \(again, can tell by the breadcrumb nav at the top what is selected\) and present you with an empty canvas to build on. However, we don't have any blocks either.

The blocks are listed on the right side of the screen. If you have an empty instance you will just see "all" with no blocks in it. To add a block, click the "Add Block" button on the right side that looks like a cloud with a down arrow in it.

Blocks are installed to instances via git URLs. In this case, we'll install a block from GitHub. Specifically, the [nio-blocks GitHub](https://github.com/nio-blocks). You can browse all of the blocks to install there, but let's start with the `Filter` block. Type the git URL to clone for the filter block `https://github.com/nio-blocks/filter.git` then click "Accept." After a brief moment, you should see the block type appear on the right side of the screen under the `Fil` group.

