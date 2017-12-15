# System Designer Reference

This section details all of the tasks that can be performed in the System Designer, nio's graphical user interface.

## Systems
System are the largest container for projects in the nio System Designer.

Systems are created in the System Designer to contain instances (running installations) of nio.

### Create a System

You can create a new system in two ways.
  1. If this is your first time opening nio, the **Create new system** window displays.

    %accordion%**Click arrow to collapse/expand image**%accordion%

    ![](/img/tasks/createnewsystem.png)

    %/accordion%

  2. If you have already been working in nio, in the lower-left corner, click the **`+`** button.

    %accordion%**Click arrow to collapse/expand image**%accordion%

    ![](/img/tasks/Hello-BlankCanvas.png)

    %/accordion%

Complete the **create new system** window:
  1. In the **system name** box, enter a meaningful name.
  1. Click **accept**.

### System Context and Toolbar

Once you create a system, you can enter the system context by clicking on a system in the system list, on the system name at the top of the navigation list, or on the system name in the breadcrumb.

In the system context you will see the system toolbar that can perform the following tasks:
  ![](/img/Toolbar-System.gif)

  Icon                      |Label             | Description      |
  --------------------------|------------------|------------------|
  ![](/img/IconEdit.gif)    |Edit              | Edit system name. View Pubkeeper configuration information.
  ![](/img/IconShare.gif)   |Share             | Share system. See more info about system sharing [here](/system-designer/sharing.html)
  ![](/img/IconDelete.gif)  |Delete            | Delete system. Instances must be deleted first.

## Instance

Instances are running versions of nio.

Instances are created inside a system and contain services.

### Create a Cloud Instance

To enter the system context, select the name of your system in the left navigation panel or on the breadcrumb above the contextual toolbar.

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/hello_nio/Hello-SelectSystemCreateInstancePoint.png)

  %/accordion%

1. Click **create cloud instance**.
1. Complete the **create cloud instance** window:

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/tasks/createcloudinstance.png)

  %/accordion%

  * In the **instance name** box, enter a meaningful name.

    > **[info] Instance Naming**
    >
    >Instance names cannot contain spaces or underscores.
1. Click **Accept**.

### Create a Local Instance

To enter the system context, select the name of your system in the left navigation panel or on the breadcrumb above the contextual toolbar.

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/hello_nio/Hello-SelectSystemCreateInstancePoint.png)

  %/accordion%

1. Click **create local instance**.
1. Complete the **create local instance** window:

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/tasks/createlocalinstance.png)

  %/accordion%

  * In the **Instance name** box, enter a meaningful name.

    > **[info] Instance Naming**
    >
    >Instance names cannot contain spaces or underscores.
  * In the **hostname** box, enter the hostname for the instance.
  * In the **port** box, enter the port number configured on the instance.
  * Leave the **access mode** as **basic**.

1. Click **accept**.

### Instance Context and Toolbar

Once you create an instance, you can enter the instance context by clicking on the instance name in the instance list or in the breadcrumb.

In the instance context you will see the the instance toolbar that can perform the following tasks:

![](/img/Toolbar-Instance.gif)

Icon                      |Label             | Description      |
--------------------------|------------------|------------------|
![](/img/IconEdit.gif)    |Edit              | Edit instance name.
![](/img/IconSave.gif)    |Save              | Save instance.
![](/img/IconDelete.gif)  |Delete            | Delete instance.


## Service

A service is a collection of blocks that work together to perform a service.

Services are created inside an instance and contain blocks.


### Create a Service

Select the name of the instance in the left navigation panel or on the breadcrumb above the contextual toolbar.

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/hello_nio/Hello-SelectInstancePoint.png)

  %/accordion%
1. Click **create new service**.
1. Complete the **create new service** window:

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/tasks/createnewservice.png)

  %/accordion%
  * In the **service name** box, enter a meaningful name.

    > **[info] Service Naming**
    >
    > Service names cannot contain the following characters: ` *  |  \ /  :  ”  <> / ? `
    >
  * Leave the **Service type** as **Service**.

1. Click **accept**.
1. Click **save** in the toolbar.

### Service Context and Toolbar

Once you create a service, you can enter the service context by clicking on the service name in the service list or in the breadcrumb.

In the service context you will see the the service toolbar that can perform the following tasks:

![](/img/Toolbar-Service.gif)

Icon                      |Label             | Description      |
--------------------------|------------------|------------------|
![](/img/IconEdit.gif)    |Edit              | Edit service name and color.
![](/img/IconSave.gif)    |Save              | Save service.
![](/img/IconStopAnim.gif)|Start/Stop        | Toggle to start and stop service.
![](/img/IconAuto.gif)    |Auto-Start On/Off | Toggle Auto-Start on and off.
![](/img/IconRevert.gif)  |Revert            | Revert changes to service.
![](/img/IconClone.gif)   |Clone             | Clone service.
![](/img/IconDelete.gif)  |Delete            | Delete service.

By default, services are set to auto-start when a nio instance is started.

## Blocks

### Add a Block

1. Click the service name in the left navigation panel or on the breadcrumb above the contextual toolbar.

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/hello_nio/Hello-SelectInstanceName.png)

  %/accordion%
1. In the **Block library** search box, enter block type name.

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/BlockLibrary.gif)

  %/accordion%

  > **[info] Block library Tabs**
  >
  > Notice that as you type, the list of installed blocks is filtered. A block can be displayed under one or more tabs.
  >
  > * The **Available** tab contains block types that are available, but may or may not have not been installed.
  > * The **Installed** tab contains block types that have been downloaded and installed. The most frequently used blocks are already pre-installed in your system.
  > * The **Configured** tab contains blocks that have already been installed, named, and configured.
1. Drag the block type to the canvas.
1. In the **Block name** box, enter a meaningful name and click **Accept**.

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/hello_nio/Hello-CreateBlockSimulate.png)

  %/accordion%

    > **[info] Block Naming**
    >
    > Block names cannot be edited after creation.
    > Block names cannot contain the following characters: `*  |  \ /  :  ”  <> / ?`
1. Click **Accept**.


## Delete a Block

1. Select the block you want to delete.
1. Click **Delete** in the toolbar.
1. Click **Delete** in the confirmation window.

## Delete a Configured Block

1. Search for the configured block in the **Block library**.
1. Click the vertical ellipsis menu and select **Delete**.
1. If the **Block in use** warning is displayed, click **Got it!** and delete the block from all services before deleting the configured block.
1. Click **Delete** in the confirmation window.

## Connect Blocks

1. Click and drag the output terminal of one block and release it on the input terminal of the next block to connect the blocks.

## Disconnect Blocks

1. Click the input terminal of the block receiving signals and drag and release it anywhere on the canvas.

## Configure Blocks

1. Double-click the block to view the configuration window.
1. Enter the required parameters.
1. Click **Accept**.

## View Logs

1. Click anywhere on the canvas to deselect the blocks.
1. Click **Start** on the toolbar.
1. Click **Open logger panel** to view the logs.

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/hello_nio/Hello-SimLogger.png)

  %/accordion%



### Service Toolbar
![](/img/Toolbar-Service.gif)

Icon                      |Label             | Description      |
--------------------------|------------------|------------------|
![](/img/IconEdit.gif)    |Edit              | Edit service name and color.
![](/img/IconSave.gif)    |Save              | Save service.
![](/img/IconStopAnim.gif)|Start/Stop        | Toggle to start and stop service.
![](/img/IconAuto.gif)    |Auto-Start On/Off | Toggle Auto-Start on and off.
![](/img/IconRevert.gif)  |Revert            | Revert changes to service.
![](/img/IconClone.gif)   |Clone             | Clone service.
![](/img/IconDelete.gif)  |Delete            | Delete service.



### Block Toolbar
![](/img/Toolbar-Block.gif)

Icon                      |Label             | Description      |
--------------------------|------------------|------------------|
![](/img/IconEdit.gif)    |Edit              | Edit block configuration.
![](/img/IconCommand.gif) |Command           | Command block.
![](/img/IconDelete.gif)  |Delete            | Delete block.

## Resources

In the upper-right corner next to your name, a navigation menu provides links to other helpful resources.

  ![](/img/tasks/helpoptions.png)
  * **docs**—reference documentation
  * **blocks**—information about all the nio blocks
  * **workshops**—self-paced tutorials
  * **support**—FAQs and contact form
  * **forum**—interact with other nio users
  * **account**—edit your profile
