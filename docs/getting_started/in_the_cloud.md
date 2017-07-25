# Running n.io in the Cloud

The easiest way to run n.io is by running it in the cloud.

To create a cloud instance:

1. Log in to the System Designer.
2. Click the "+" icon on the lower left corner to create and name a new system.
3. Click "Accept."
4. Select the name of the system you created.
5. Click "Create a Cloud Instance."
6. Type the name of the instance, leave the instance type as n.io cloud, and click "Accept".
7. Wait for the instance to spin-up and note the name of the new instance on the left side of the screen.

## Add a Service and Blocks

You now have an instance, but it is empty, let's fix that! 

To add a service:

1. Select the name of the instance you created.
2. Click "Add New Service."
3. Type the name of the service, leave the service type as Service, and click "Accept."

You now have an empty canvas to build, but we do not have any blocks yet.

Blocks are installed to instances via git URLs. Specifically, [nio-blocks GitHub](https://github.com/nio-blocks) is the repository of the blocks created by n.io.  Browse and search the blocks to determine the function you want to produce. For example, the `Filter` block is located at the git URL `https://github.com/nio-blocks/filter.git` . 

To add a block:

1. Click "All" on the right side of the screen. If you have an empty instance, no blocks will be displayed.
2. Click the Add Block icon which looks like a cloud with an arrow.
3. To import the block, enter the Github clone URL of the block and click "Accept."
4. After uploading, the block type displays on the right side of the screen under its group.



