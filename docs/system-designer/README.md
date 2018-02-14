# <span class="allow-caps">System Designer</span> introduction

The nio System Designer is the graphical user interface used to build your nio system.

{% video %}https://www.youtube.com/watch?v=GFs5EK6zao8{% endvideo %}

> The [System Designer workshop](https://workshops.n.io/system-designer) provides a good introduction to using the System Designer to build your first service.

---
## <span class="allow-caps">System Designer</span> navigation

<img class="left" src="/img/system-designer-overview.png" height="375" />

### Systems list
The systems list is the leftmost column in the designer.
* The designer automatically creates an abbreviation for each system name.
* To create a system, click the **`+`** button in the lower-left corner.
* To change into the system context and view a system, click the system name.
* Learn more about [systems](/systems).

### Instances and services list
The instances and services list is located to the right side of the systems column.
* To view the services within an instance, click the arrow next to the instance name.
    * The list of services displays below the instance name.
* To view the contents of an instance in the canvas, click the instance name.
* To enter the service context and view the contents of a service, click a service name.
* Learn more about [instances](/instances) and [services](/services).

### Breadcrumb
The breadcrumb is located at the top of the System Designer.
* As you navigate from system to service, the breadcrumb allows you to easily identify your location in the system.

<img class="left" src="/img/cloud/hierarchy.gif" width="600" />

### Contextual toolbar
The contextual toolbar is located underneath the breadcrumb.
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

### Canvas (service or block workflow graph)
The canvas is located in the center of the System Designer.
* The canvas shows the content of either an instance or a service, depending on the context.
* In the instance context, the canvas shows the interactions of the services in your instance.
    * To view the service workflow graph in the canvas, click the instance name.
* In the service context, the canvas shows the interactions of blocks in your service.
    * The block workflow is designed by the user and represents the flow of data between the inputs and outputs of the [blocks](/blocks/README.md) in a service.
    * To view a service's block workflow in the canvas, click the service's name.
    * To add a block to the service, install and then drag and drop a block from the block library onto the canvas.
    * Connect the blocks from output to input to create the block workflow.

### Block library
The block library is located on the far right of the System Designer.
* The block library is visible in the service context.
* The block library contains blocks that are available for you to use to build the logic in your service.
* In the search box, enter the name of a block. As you type, the list of blocks is filtered.
