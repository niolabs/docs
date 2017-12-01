# System Designer Basics

The System Designer is the graphical user interface used to build your nio system. This overview provides you with a quick tour of the basics of creating a system, instance, service, and block.


## Get Help

1. Click the menu in the upper-right corner next to your name.
1. Select one of the available options:

  ![](/img/tasks/helpoptions.png)
  * **docs** - reference documentation
  * **blocks** - information on all of the nio blocks
  * **workshops** - self-paced tutorials
  * **support** - FAQs and contact form
  * **forum** - interact with other nio users
  * **account** - edit your profile

## Systems

### Create a System

1. You can create a new system in two ways.
  * If this is your first time opening nio, the **Create new system** window displays.

    %accordion%**Click arrow to collapse/expand image**%accordion%

    ![](/img/tasks/createnewsystem.png)

    %/accordion%

  * If you have already been working in nio, in the lower-left corner, click the **`+`** button.

    %accordion%**Click arrow to collapse/expand image**%accordion%

    ![](/img/tasks/Hello-BlankCanvas.png)

    %/accordion%

1. Complete the **Create new system** window:
  1. In the **System name** box, enter a meaningful name.
  1. Click **Accept**.

### Delete a System

1. Select the system name.
1. Click **Delete** in the toolbar.
1. If you the **Cannot delete system** message is displayed, you must delete the instances before deleting the system.
1. Click **Delete**.

## Instance

### Create a Cloud Instance

1. Select the name of your system in the left navigation panel or on the breadcrumb above the contextual toolbar.

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/hello_nio/Hello-SelectSystemCreateInstancePoint.png)

  %/accordion%

  > **[info] Breadcrumb**
  >
  > ![](/img/hello_nio/hierarchy.gif)
  >
  > Click on a hyperlink in the breadcrumb above the toolbar to navigate between the levels of your system. The breadcrumb allows you to visualize your location in the project.
1. Click **Create cloud instance**.
1. Complete the **Create cloud instance** window:

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/tasks/createcloudinstance.png)

  %/accordion%

  * In the **Instance name** box, enter a meaningful name.

    > **[info] Instance Naming**
    >
    >Instance names cannot contain spaces or underscores.
1. Click **Accept**.

### Create a Local Instance

1. Select the name of your system in the left navigation panel or on the breadcrumb above the contextual toolbar.

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/hello_nio/Hello-SelectSystemCreateInstancePoint.png)

  %/accordion%

1. Click **Create local instance**.
1. Complete the **Create local instance** window:

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/tasks/createlocalinstance.png)

  %/accordion%

  * In the **Instance name** box, enter a meaningful name.

    > **[info] Instance Naming**
    >
    >Instance names cannot contain spaces or underscores.
  * In the **Hostname** box, enter the hostname.
  * In the **Port** box, enter the port number.
  * Leave the **Access mode** as **basic**.

1. Click **Accept**.

## Service

### Create a Service

1. Select the name of the instance in the left navigation panel or on the breadcrumb above the contextual toolbar.

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/hello_nio/Hello-SelectInstancePoint.png)

  %/accordion%
1. Click **Create new service**.
1. Complete the **Create new service** window:

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/tasks/createnewservice.png)

  %/accordion%
  * In the **Service name** box, enter a meaningful name.

    > **[info] Service Naming**
    >
    > Service names cannot contain the following characters: ` *  |  \ /  :  ”  <> / ? `
    >
  * Leave the **Service type** as **Service**.

1. Click **Accept**.
1. Click **Save** in the toolbar.
  >**[info] Contextual Toolbar Functions**
  >
  >Hover over each icon on the contextual toolbar to display its function. The available functions change depending on your location in the project.
  >
  >![](/img/Toolbar-Service.gif)
1. Click **Auto-Start Off** in the toolbar.

  By default, services are set to auto-start when a nio instance is started.
1. Optional. Click **Edit** in the toolbar, select one of the colored circles to represent this service, and click **Accept**.

  By default, the color of a service is white. Color coding your services can help you keep your instances organized when working on larger projects with multiple instances.

  %accordion%**Click arrow to collapse/expand image**%accordion%

  ![](/img/hello_nio/Hello-EditServiceColor.png)

  %/accordion%

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

## Contextual Toolbar
The contextual toolbar changes based on your location in the project to represent the available functions. Hover over the icon to reveal the name of the icon. Some icons have dual functions where you click to toggle an action, such as starting and stopping a service.

Icon                      |Description       |
--------------------------|------------------|
![](/img/IconAuto.gif)    |Auto-Start On/Off
![](/img/IconClone.gif)   |Clone             
![](/img/IconCommand.gif) |Command           
![](/img/IconDelete.gif)  |Delete            
![](/img/IconEdit.gif)    |Edit              
![](/img/IconRevert.gif)  |Revert            
![](/img/IconSave.gif)    |Save              
![](/img/IconShare.gif)   |Share             
![](/img/IconStopAnim.gif)|Start/Stop        

### System Toolbar
![](/img/Toolbar-System.gif)

Icon                      |Label             | Description      |
--------------------------|------------------|------------------|
![](/img/IconEdit.gif)    |Edit              | Edit system name. View Pubkeeper configuration information.
![](/img/IconShare.gif)   |Share             | Share system.
![](/img/IconDelete.gif)  |Delete            | Delete system. Instances must be deleted first.

### Instance Toolbar
![](/img/Toolbar-Instance.gif)

Icon                      |Label             | Description      |
--------------------------|------------------|------------------|
![](/img/IconEdit.gif)    |Edit              | Edit instance name.
![](/img/IconSave.gif)    |Save              | Save instance.
![](/img/IconDelete.gif)  |Delete            | Delete instance.


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
