# System Designer Introduction

The nio System Designer is the graphical user interface used to build your nio system. This overview provides you with a quick tour of the user interface including the navigation, work areas, and toolbars.


{% video %}https://www.youtube.com/watch?v=GFs5EK6zao8{% endvideo %}

## System Designer Navigation

The screen of the System Designer is laid out in three columns with the systems column and instances and services list on the left; breadcrumb, contextual toolbar, and canvas in the middle; and the block library on the right.

![map of System Designer](/img/system-designer-overview.png)

### Systems Column

A list of [systems](/systems/README.md) is displayed in a column on the left side of the screen. The designer automatically creates an abbreviation for each system name.

To create a system, click the **`+`** button in the lower-left corner.

To change into the system context and view a system, click the system name.

### Instances and Services List

A list of [instances](/instances/README.md) is displayed in the left navigation panel next to the systems column.

To view the list of [services](/services/README.md) within an instance, click the arrow next to the instance name. The list of services displays below the instance name.

To change into the instance context and view the contents of an instance in the canvas, click the instance name.

To enter the service context and view the contents of a service in the canvas, click a service name.

### Breadcrumb

As you travel up and down the levels of your system, note that the breadcrumb changes allowing you to easily identify your location in the system.

![breadcrumb hierarchy](/img/cloud/hierarchy.gif)

### Contextual Toolbar

The contextual toolbar changes based on your location in the project displays the available functions. Hover over the icon to reveal the name of the icon. Some icons have a dual appearance when you toggle an action, such as starting and stopping a service.

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

The canvas shows the content of either an instance or a service, depending on the context. In the instance context, the canvas shows the graph of the services in your instance. In the service context, the canvas shows the graph of blocks in your service.

#### Instance context

In the instance context, the canvas displays a service workflow graph that represents the interactions between the services in an instance.

To view the service workflow graph in the canvas, click the instance name.

#### Service context

In the service context, the canvas displays the interactive block workflow.

The block workflow is designed by the user and represents the flow of data between the inputs and outputs of the [blocks](/blocks/README.md) in a service.

To view a service's block workflow in the canvas, click the service's name.

To add a block to the service, install and then drag and drop a block from the block library on to the canvas.

Connect the blocks from output to input to create the block workflow.

### Block Library

The block library is visible in the service context.

The block library contains blocks that are available for you to use to build the logic in your service.

In the search box, enter the name of a block. As you type, the list of blocks is filtered.
