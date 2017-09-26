# System Designer Tasks

The System Designer is the graphical user interface used to build your {{ book.product }} system. This overview provides you with a quick tour of the user interface including the navigation, work areas, and toolbars.

# h1 Heading
## h2 Heading
### h3 Heading
#### h4 Heading
##### h5 Heading
###### h6 Heading

We'll paint one happy little tree right here. Let's do it again then, what the heck. We'll put some happy little leaves here and there.

1. Do this (1)
1. Do this (1)
  1. Do this (1)
  1. Do this (1)

We'll paint one happy little tree right here. Let's do it again then, what the heck. We'll put some happy little leaves here and there.

1. Do this (1)
1. Do this (1)
  * Do this (+)
  * Do this (+)

We'll paint one happy little tree right here. Let's do it again then, what the heck. We'll put some happy little leaves here and there.

1. Do this (1)
1. Do this (1)
  + Do this (+2)
  + Do this (+2)

We'll paint one happy little tree right here. Let's do it again then, what the heck. We'll put some happy little leaves here and there.

* Level 1 one (+)
* Level 1 one (+)
  * Level 2 two (+)
    * Level 3 three (+)
      * Level 4 four (+)

## Project Hierarchy
![](/img/ProjectHierarchy.gif)

## Contextual Toolbar

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
![](/img/IconEdit.gif)    |Edit              | Edit system. View Pubkeeper configuration information.
![](/img/IconShare.gif)   |Share             | Share system.
![](/img/IconDelete.gif)  |Delete            | Delete system. Instances must be deleted first.

### Instance Toolbar
![](/img/Toolbar-Instance.gif)

Icon                      |Label             | Description      |
--------------------------|------------------|------------------|
![](/img/IconEdit.gif)    |Edit              | Edit instance.
![](/img/IconSave.gif)    |Save              | Save instance.
![](/img/IconDelete.gif)  |Delete            | Delete instance.


### Service Toolbar
![](/img/Toolbar-Service.gif)

Icon                      |Label             | Description      |
--------------------------|------------------|------------------|
![](/img/IconEdit.gif)    |Edit              | Edit service. Colorize
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
![](/img/IconSave.gif)    |Save              | Save block.
![](/img/IconCommand.gif) |Command           | Command block.
![](/img/IconRevert.gif)  |Revert            | Revert changes to block including deletion.
![](/img/IconDelete.gif)  |Delete            | Delete block.

## Blocks

### Block Library
![](/img/BlockLibrary.gif)

### Connect and Disconnect blocks
![](/img/JoinUnjoin.gif)


# Systems

## Create a System

The very first time you open the {{ book.product }} platform, you are literally starting with a blank canvas. This is where start building a system containing instances and blocks.

1. Open the **System Designer** in a new tab.

  https://designer.n.io/

1. In the lower-left corner, click the **`+`** button to build.

  %accordion%**Click arrow to expand image**%accordion%

  ![](/img/hello_nio/Hello-BlankCanvas.png)

  %/accordion%

1. Complete the **Create a new system** window:
1. Click **Accept**.

  %accordion%**Click arrow to expand image**%accordion%

  ![](/img/hello_nio/Hello-CreateNewSystem.png)

  %/accordion%

* In the **System name** box, enter a meaningful name.
* Choose your Pubkeeper configuration:
  1. Auto (recommended)
  1. Advanced (advanced users only)
    * Hostname
    * Port
    * Token
    * Secure
  1. None (advanced users only)
1. Click **Accept**.


# Instance

## Create a Cloud Instance
Now you are ready to create an instance named `Tutorials`.

1. Select the name of your **workshops** system in the left navigation panel or on the breadcrumb above the contextual toolbar.

  %accordion%**Click arrow to expand image**%accordion%

  ![](/img/hello_nio/Hello-SelectSystemCreateInstancePoint.png)

  %/accordion%

  > **[info] Breadcrumb**
  >
  > ![](/img/hello_nio/hierarchy.gif)
  >
  > Click on a hyperlink in the breadcrumb above the toolbar to navigate between the levels of your system. The breadcrumb allows you to visualize your location in the project.
1. Click **Create a cloud instance**.
1. Complete the **Create a new cloud instance** window:

  %accordion%**Click arrow to expand image**%accordion%

  ![](/img/hello_nio/Hello-CreateCloudInstance.png)

  %/accordion%

  * In the **Instance name** box, enter `Tutorials`.
  * Leave the **Instance type** as **n.io Cloud**.

  > **[info] Instance Naming**
  >
  >Instance names cannot contain spaces or underscores.
1. Click **Accept**.

Alright! You just created a cloud [instance](https://docs.n.io/glossary#instance) of nio. You will create all of your [services](https://docs.n.io/glossary#service) for the tutorials within this cloud instance. In the next step you will learn how to make your first service.

# Service

## Create a service
Now you are ready to create a simple service named `simulate-and-log`.

1. Select the name of the **Tutorials** instance under **workshops** in the left navigation panel or on the breadcrumb above the contextual toolbar.

  %accordion%**Click arrow to expand image**%accordion%

  ![](/img/hello_nio/Hello-SelectInstancePoint.png)

  %/accordion%
1. Click **Add new service**.
1. Complete the **Create new service** window:

  %accordion%**Click arrow to expand image**%accordion%

  ![](/img/hello_nio/Hello-CreateNewService.png)

  %/accordion%
  * In the **Service name** box, enter `simulate-and-log`.
  * Leave the **Service type** as **Service**.

  > **[info] Service Naming**
  >
  > Service names cannot contain the following characters: ` *  |  \ /  :  ”  <> / ? `
  >
1. Click **Accept**.
1. Click **Save** in the toolbar.
  >**[info] Contextual Toolbar Functions**
  >
  >Hover over each icon on the contextual toolbar to display its function. The available functions change depending on your location in the project.
  >
  >![](/img/hovertoolbar.gif)
1. Click **Auto-Start Off** in the toolbar.

  By default, services are set to auto-start when a {{ book.product }} instance is started.
1. Click **Edit** in the toolbar.
1. Optional. Select one of the colored circles to represent this service and click **Accept**.

  By default, the color of a service is white. Color coding your services can help you keep your instances organized when working on larger projects with multiple instances.

  %accordion%**Click arrow to expand image**%accordion%

  ![](/img/hello_nio/Hello-EditServiceColor.png)

  %/accordion%

You’re cruising now! You just created your first [service](https://docs.n.io/glossary#service). A service is a real-time process that runs on an instance. The logic is configured as a workflow of [blocks](https://docs.n.io/glossary#block) which you will now create in Step 4.

# Blocks

## Add Blocks
Now you will add two pre-installed blocks to your `simulate-and-log`  service. The _CounterIntervalSimulator_ block simulates and emits a [signal](https://docs.n.io/glossary/#signal)  at a specified interval in seconds. The _Logger_ block logs each incoming signal.

| Block Type           | Block Name                |
|----------------------|---------------------------|
| [CounterIntervalSimulator](https://blocks.n.io/CounterIntervalSimulator) | Simulate |
| [Logger](https://blocks.n.io/Logger) | Log       |

1. Click the `simulate-and-log` Service Name under **Tutorials** in the left navigation panel or on the breadcrumb above the contextual toolbar.

  %accordion%**Click arrow to expand image**%accordion%

  ![](/img/hello_nio/Hello-SelectInstanceName.png)

  %/accordion%
1. In the **Block library** search box, enter `CounterIntervalSimulator`. Since `CounterIntervalSimulator` is one of the pre-installed block types, the block type displays under the **Installed** tab.  

  %accordion%**Click arrow to expand image**%accordion%

  ![](/img/BlockLibrary.gif)

  %/accordion%

  > **[info] Block Library Tabs**
  >
  > Notice that as you type, the list of installed blocks is filtered. A block can be displayed under one or more tabs.
  >
  > * The **Available** tab contains block types that are available, but may or may not have not been installed.
  > * The **Installed** tab contains block types that have been downloaded and installed. The most frequently used blocks are already pre-installed in your system.
  > * The **Configured** tab contains blocks that have already been installed, named, and configured.
1. Drag the **CounterIntervalSimulator** block type to the canvas.
1. In the **Block name** box, enter `Simulate` and click **Accept**.

  %accordion%**Click arrow to expand image**%accordion%

  ![](/img/hello_nio/Hello-CreateBlockSimulate.png)

  %/accordion%

  > **[info] Block Naming**
  >
  > Block names cannot be edited after creation.
  > Block names cannot contain the following characters: `*  |  \ /  :  ”  <> / ?`
1. In the **Block library** search box, enter `Logger`.
1. Drag the **Logger** block type to the canvas.
1. In the **Block name** box, enter `Log` and click **Accept**.

  %accordion%**Click arrow to expand image**%accordion%

  ![](/img/hello_nio/Hello-Blockname-Log.png)

  %/accordion%

To learn about all the blocks {{ book.product }} has to offer, visit [https://blocks.n.io](https://blocks.n.io).

Way to go! You are now familiar with how to add, name, and save the most basic building “blocks” of a nio system - no pun intended! The first block will simulate data and the second will log that data. Let’s make that happen!

## Step 5: Connect the Blocks
Now you have two blocks that need to communicate. In {{ book.product }}, this is accomplished by simply connecting the output terminal of one block to the input terminal of another block. The lines connecting the blocks together configure the route the signal will take.

1. Click and drag the output terminal of the **Simulate** block and release it on the input terminal of the **Log**  block to connect the blocks.

  %accordion%**Click arrow to expand image**%accordion%

  ![](/img/hello_nio/Hello-ConnectAndSaveBlocks.png)

  %/accordion%
1. Select the **Simulate** block, and click **Save** on the toolbar.
1. Select the **Log** block, and click **Save** on the toolbar.

>**[info] Disconnecting Blocks**
>
>To disconnect two blocks, click the input terminal of the block receiving signals and drag and release it anywhere on the canvas.

Now that you connected the two blocks, you need to configure each one to do exactly what you want.

## Step 6: Configure Blocks and Run Service
Now you can start your first service.

1. Click anywhere on the canvas to deselect the blocks.
1. Click **Start** on the toolbar.
1. Click **Open logger panel** to view the logs. The logs are displayed with the default settings.

  %accordion%**Click arrow to expand image**%accordion%

  ![](/img/hello_nio/Hello-SimLogger.png)

  %/accordion%






Icon                      |Description       |
--------------------------|------------------|
![](/img/IconDownload.gif)    |Download block
![](/img/IconBlockLibrary.gif)|Block Library


%accordion%Some title here%accordion%

Any content here

%/accordion%

> Use this for help for beginners--informational messages that add to the learning experience. Do not place steps in this message.


## INVALID CHARACTERS




Info styling

> **[info] For beginners/tips**
>
> Use this for help for beginners--informational messages that add to the learning experience. Do not place steps in this message.

Warning styling

> **[warning] For warning**
>
> Use this for warning messages.

Danger styling

> **[danger] For danger**
>
> Use this for danger messages. Use sparingly.

Success styling

> **[success] For success**
>
> Use this for success messages. Also, for items needed in tutorials before you begin.

Common C++ Naming Conventions

Types start with upper case: MyClass.
Functions and variables start with lower case: myMethod.
Constants are all upper case: const double PI=3.14159265358979323;.
C++ Standard Library (and other well-known C++ libraries like Boost) use these guidelines:
Macro names use upper case with underscores: INT_MAX.
Template parameter names use camel case: InputIterator.
All other names use snake case: unordered_map.


> Use this for help for beginners--informational messages that add to the learning experience. Do not place steps in this message.

- [ ] Open
- [x] Closed
