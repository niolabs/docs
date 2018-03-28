# <span class="allow-caps">System Designer</span> reference

This section details all of the tasks that can be performed in the nio System Designer, and is organized by context:
 - [system](#system-sd)
 - [instance](#instance-sd)
 - [service](#service-sd)
 - [block](#blocks-sd)

It can help you answer questions about what you can do in each level of the System Designer as you navigate from creating a system, to editing an instance name, to deleting a block.

---

## System {#system-sd}
[Systems](/systems/README.md) are the largest container for projects in the nio System Designer.

Systems are created in the System Designer to contain instances (running installations) of the nio Platform.

### Create a system

<img class="right border" src="/img/cloud/Hello-CreateNewSystem.gif" width="250" />

From the **System Designer** (https://designer.n.io/), you can create a new system in two ways.
  * If this is your first time opening the System Designer, the **create new system** modal window displays automatically.
  * If it doesn't open automatically, click the **`+`** button in the lower-left corner of the designer.


Complete the **create new system** modal:
  * In the **system name** box, enter a name for your system.
  * In the **template** dropdown, you can keep the default blank system or select a system template.
  * Click **accept**.

  ####&nbsp;

> **[info] System names**
>
> The System Designer automatically creates an abbreviation for each system name.
>
> Tip: try using an acronym for your system name.


### System edit, share, delete

Once you create a nio system, you can enter the system context by clicking either the system in the system list, the system name at the top of the navigation list, or the system name in the breadcrumb.

<img class="left" src="/img/cloud/Hello-SelectSystemCreateInstancePoint.png" width="600" />


In the system context you will see the system toolbar that can perform the following tasks:

<img class="left" src="/img/Toolbar-System.gif" height="75" />

  Icon                      |Label             | Description      |
  --------------------------|------------------|------------------|
  ![](/img/IconEdit.gif)    |edit              | Edit system name. View Pubkeeper configuration information.
  ![](/img/IconShare.gif)   |share             | Share system. This option is only available to teams within an organization. Read more information about system sharing [here](/organizations/management.md#sharing).
  ![](/img/IconDelete.gif)  |delete            | Delete system. Instances must be deleted first.

---

## Instance {#instance-sd}

[Instances](/instances/README.md) are running versions of nio.

Instances are created inside a system and contain services.

### Create an instance in the cloud

To enter the system context, select the name of your system in the left navigation panel or on the breadcrumb above the contextual toolbar.
<br>
<img class="right border" src="/img/tasks/createcloudinstance.png" width="250" /><img class="left" src="/img/cloud/Hello-SelectSystemCreateInstancePoint.png" width="500" />
1. Click **create cloud instance**.
1. Complete the **create cloud instance** modal:
  * In the **instance name** box, enter a meaningful name.
1. Click **accept**.


### Connect to a local instance

To enter the system context, select the name of your system in the left navigation panel or on the breadcrumb above the contextual toolbar.
<br>
<img class="right border" src="/img/tasks/createlocalinstance.png" width="250" />
<img class="left" src="/img/cloud/Hello-SelectSystemCreateInstancePoint.png" width="500" />

1. Click **create local instance**.
1. Complete the **create local instance** modal:
  * **instance name**: enter a meaningful name.
  * **hostname**: enter the hostname for the instance.
  * **port**: enter the port number configured on the instance.
  * **access mode**: leave as **basic**.
1. Click **accept**.

<br>

> **[info] Instance names**
>
> Instance names cannot contain spaces or underscores.

### Instance edit, save, delete

Once you create an instance, you can enter the instance context by clicking the instance name in the instance list or in the breadcrumb.

<img class="left" src="/img/cloud/Hello-SelectInstancePoint.png" width="600" />

In the instance context you will see the the instance toolbar and can perform the following tasks:

<img class="left" src="/img/Toolbar-Instance.gif" height="75" />

Icon                      |Label             | Description      |
--------------------------|------------------|------------------|
![](/img/IconEdit.gif)    |edit              | Edit instance name and set environment variables.
![](/img/IconSave.gif)    |save              | Save instance.
![](/img/IconDelete.gif)  |delete            | Delete instance.

## {#instance-env}
> <img class="right border" src="/img/tasks/editcloudinstance.png" width="200" />
> **[info] Environment variables**


> The environment variables section in the edit instance modal window can be used to set instance-wide variables.
> This is useful for storing values such as API keys/secrets or other variables that you do not want to hardcode directly into block properties.
>
> Only admin-level users can view/edit the values of the environment variables in the edit instance modal.
>
> More information about environment variables can be found here: [docs.n.io/instances/environment-variables.html](/instances/environment-variables.md).
> <br>


---

## Service {#service-sd}

A nio [service](/services/README.md) is a user-configurable signal path that connects a collection of blocks so they can work together to perform a desired task or service.

Services are created inside an instance and contain blocks.

### Create a service

Select the name of the instance in the left navigation panel or on the breadcrumb above the contextual toolbar.
<br>
<img class="right border" src="/img/tasks/createnewservice.png" width="250" />
<img class="left" src="/img/cloud/Hello-SelectInstancePoint.png" width="500" />

1. Click **create new service**.
1. Complete the **create new service** modal:
  * In the **service name** box, enter a meaningful name.
  * Leave the **service type** as **Service**.
1. Click **accept**.
1. Click **save** in the toolbar.

> **[info] Service names**
>
> Service names cannot contain the following characters: ` *  |  \ /  :  ”  <> / ? `
>

### Service edit, save, start/stop, auto-start, revert, clone, delete

Once you create a service, you can enter the service context by clicking the service name in the service list or by double clicking the service in the canvas.

In the service context you will see the the service toolbar that can perform the following tasks:

<img class="left" src="/img/Toolbar-Service.gif" height="75" />

Icon                      |Label             | Description      |
--------------------------|------------------|------------------|
![](/img/IconEdit.gif)    |edit              | Edit service name and color.
![](/img/IconSave.gif)    |save              | Save service.
![](/img/IconStopAnim.gif)|start/stop        | Toggle to start and stop service.
![](/img/IconAuto.gif)    |auto-start on/off | Toggle Auto-Start on and off. Default is on.
![](/img/IconRevert.gif)  |revert            | Revert changes to service.
![](/img/IconClone.gif)   |clone             | Clone service.
![](/img/IconDelete.gif)  |delete            | Delete service.


### Connect/disconnect blocks

The signal paths between blocks are part of the service-level configuration. If you change the connections between your blocks, you will need to save your service in the service toolbar.

To connect two blocks, click and drag the output terminal of one block and release the connector on the input terminal of the next block.

To disconnect, click the input terminal of the block receiving signals and drag and release the connector anywhere on the canvas.

### View logs

Logs show the output of a running service.

To view the logger panel, click anywhere on the canvas to deselect the blocks and enter the service context.
1. Click **start** on the toolbar to run your service.
1. Click **open logger panel** to view the logs.

<img class="left" src="/img/cloud/Hello-SimLogger.gif" />


---

## <a name="blocks-sd">Blocks</a> {#blocks-sd}

[Blocks](/blocks/README.md) are the units of work inside a nio service.

### Add a block

Click the service name in the service list or on the breadcrumb above the contextual toolbar to enter the service context.

<img class="left" src="/img/cloud/Hello-SelectInstanceName.png" width="600" />

In the **block library** search box, enter a block type name.


<img class="left" src="/img/BlockLibrary.gif" />


  > **[info] Block library tabs**
  >
  > Notice that as you type, the list of installed blocks is filtered. A block can be displayed under one or more tabs.
  >
  > * The **available** tab contains block types that are available, but may or may not have not been installed.
  > * The **installed** tab contains block types that have been downloaded and installed. The most frequently used blocks come pre-installed in your system.
  > * The **configured** tab contains blocks that have already been installed, named, and configured.

1. Drag the block type to the canvas.
1. In the **block name** box, enter a meaningful name and click **accept**.
<img class="left border" src="/img/cloud/Hello-CreateBlockSimulate.png" width="250" />

> **[info] Block names**
>
> Block names cannot be edited after creation.
>
> Block names cannot contain the following characters: `*  |  \ /  :  ”  <> / ?`

### Block edit, command, delete

Once you have added a block, you can enter the block context by clicking the block.

In the block context you will see the the block toolbar that can perform the following tasks:

<img class="left" src="/img/Toolbar-Block.gif" height="75" />

Icon                      |Label             | Description      |
--------------------------|------------------|------------------|
![](/img/IconEdit.gif)    |edit              | Edit block configuration.
![](/img/IconCommand.gif) |command           | Command block.
![](/img/IconDelete.gif)  |delete            | Delete block.


### Delete a configured block

1. Search for the configured block in the **block library**.
1. Click the vertical ellipsis menu and select **delete**.
1. If the **block in use** warning is displayed, click **got it!** and delete the block from all services before deleting the configured block.
1. Click **delete** in the block confirmation modal window.

### Configure blocks

1. Double-click the block to view the block configuration modal.
1. Enter the required parameters.
1. Click **accept**.

---

## Additional resources

In the upper-right corner next to your name, a navigation menu provides links to other helpful resources.

<img class="left" src="/img/tasks/helpoptions.png" />

  * [**docs**](https://docs.n.io)—reference documentation
  * [**blocks**](https://blocks.n.io)—information about all the nio blocks
  * [**workshops**](https://workshops.n.io)—self-paced tutorials
  * [**support**](https://account.n.io/support)—FAQs and contact form
  * [**forum**](https://forum.n.io)—interact with other nio users
  * [**account**](https://account.n.io/settings)—edit your profile
