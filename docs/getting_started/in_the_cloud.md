# Running {{ book.product }} in the Cloud

The easiest way to run {{ book.product }} is by running it in the cloud.

To create a cloud instance:

1. Log in to the System Designer.
2. Click the **+** button in the lower-left corner to create and name a new system.
3. Click **Accept**.
4. Select the name of the system.
5. Click **Create a Cloud Instance**.
6. Type the name of the instance, leave the instance type as **n.io Cloud**, and click **Accept**.
7. Wait for the instance to spin-up and note the name of the new instance on the left side.

## Add a Service

You now have an instance, but it is empty. Let's fix that!

To add a service:

1. Select the name of the instance.
2. Click **Add New Service**.
3. Type the name of the service, leave the service type as **Service**, and click **Accept**.

## Add Blocks

You now have an empty canvas, and now you are ready for blocks.



Blocks are installed to instances using git URLs. Specifically, the [nio-blocks GitHub repository](https://github.com/nio-blocks) is the collection of blocks created by {{ book.product }}.  Browse and search the blocks to determine the function you want to use. For example, the `Filter` block is located at `https://github.com/nio-blocks/filter.git` .

To add a block:

1. Click the **Block Library** in the upper-right corner.
2. In the Search box, enter the name of a block. As you type, the list is filtered.
3. Click the **Install Block** button which resembles a cloud with a down arrow.
3. Drag the **Logger** block onto the canvas.
5. Name the block and click **Accept**. 