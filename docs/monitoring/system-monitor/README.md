# <span class="allow-caps">System Monitoring</span> introduction

The nio system monitoring application, found at [app.n.io/monitor](https://app.n.io/monitor), is the graphical user interface used to monitor your running nio systems.


Access the System Monitor by clicking the monitor icon in the application switcher in the far left column.

<img class="left" src="/img/tasks/monitorApp.png" width="300" />

---
## <span class="allow-caps">System Monitor</span> overview

<img class="left" src="/img/system-monitor-overview.png" height="375" />

### App switcher
The leftmost column shows the app switcher that enables you to switch between applications. If your license includes monitoring, you can view the system monitoring tool by clicking the monitor icon.

### Systems list
The systems list is located on the left side of the System Monitor.
* To view the instances within a system, click the system name.

### Instance cards
All instances within a selected system will display as cards in the System Monitor. Each instance card contains the name of the instance, hostname, and port that the instance is running on.
* Instances with issues:
  * Any instances with issues will display under this section. All issues that put the instance in this state will display under **Issues**.
* Instances without issues:
  * All instances without issues will display under this section.

### Viewing instance logs
Additional issue details and error logs can be viewed by clicking on the instance card. This view provides a logger pannel which defaults to viewing logs in an *error* state. Other useful information includes instance uptime and the version of the nio Platform that is running on the instance. 

<img class="left" src="/img/tasks/monitorlogger.png" />

### Auto refresh
The auto refresh toggle is located at the top of the system view. When on, the system monitoring tool will poll instances every 5 minutes for status information. When this toggle is off, the system monitoring tool will need to be refreshed to see any new issues on instances. 

<img class="center" src="/img/tasks/monitorautorefresh.png" />

### Header navigation

In the header you can switch between organizations with the organization dropdown, navigate to other parts of niolabs with the navigation menu, and logout of your account.

<img class="left" src="/img/tasks/monitorhelpoptions.png" />

  * [**docs**](https://docs.n.io)—reference documentation
  * [**blocks**](https://blocks.n.io)—information about all the nio blocks
  * [**workshops**](https://workshops.n.io)—self-paced tutorials
  * [**support**](https://account.n.io/support)—FAQs and contact form
  * [**forum**](https://forum.n.io)—interact with other nio users
  * [**binaries**](https://account.n.io/binaries/download)—download the nio binary


### Support
Click the intercom icon for support at any time.
