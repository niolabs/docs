# System Designer Introduction

The nio System Designer is the graphical user interface used to build your nio system.

> Take the [nio System Designer Workshop](https://workshops.n.io/system-designer) to go hands-on with the system Designer

---
## System Designer Navigation

<center>
<img src="/img/system-designer-overview.png" height="350" vspace="10" />
</center>

### Systems List
* The designer automatically creates an abbreviation for each system name.
* To create a system, click the **`+`** button in the lower-left corner.
* To change into the system context and view a system, click the system name.
* Learn more about [systems](/systems)

### Instances and Services List
* To the right of the systems column.
* To view the  within an instance, click the arrow next to the instance name.
    * The list of services displays below the instance name.
* To view the contents of an instance in the canvas, click the instance name.
* To enter the service context and view the contents of a service, click a service name.
* Learn more about [instances](/instances) and [services](/services)

### Breadcrumb
* As you navigate from system to service, the breadcrumb allows you to easily identify your location in the system.

<center>
<img src="/img/cloud/hierarchy.gif" height="150" vspace="10" />
</center>

### Contextual Toolbar
* The contextual toolbar changes based on your location in the project, and displays the available functions.
* Hover over the icon to reveal the name of the icon.
* Some icons have a dual appearance when you toggle an action, such as starting and stopping a service.

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

### Canvas (Service or Block Workflow Graph)
* The canvas shows the content of either an instance or a service, depending on the context.
* In the instance context, the canvas shows the interactions of the services in your instance.
    * To view the service workflow graph in the canvas, click the instance name.
* In the service context, the canvas shows the interactions of blocks in your service.
    * The block workflow is designed by the user and represents the flow of data between the inputs and outputs of the [blocks](/blocks/README.md) in a service.
    * To view a service's block workflow in the canvas, click the service's name.
    * To add a block to the service, install and then drag and drop a block from the block library on to the canvas.
    * Connect the blocks from output to input to create the block workflow.

### Block Library
* The block library is visible in the service context.
* The block library contains blocks that are available for you to use to build the logic in your service.
* In the search box, enter the name of a block. As you type, the list of blocks is filtered.
