# nio-managed cloud instance

While the true power of the nio Platform is experienced when you have multiple [local installations](/running-nio/locally.md) communicating across a distributed network, we also offer the ability to spin up nio-managed cloud instances through the **nio System Designer**.

A nio-managed cloud instance allows you to get up and running quickly and to start building services right away.

You can also choose to start with one of our [system templates](https://workshops.n.io/system-templates) to quickly explore and configure annotated, pre-built systems.

>**[info] Prerequisites**
>
>* **A nio account**: [Sign up here](https://account.n.io/signup)

---

## Create a system
<img class="right border" src="/img/cloud/add-system.png" width="250" />

A system is a group of interrelated elements. In the nio System Designer, a system contains interrelated nio instances. Think of it as a workspace where you can put related projects.
1. Open the **System Designer**: https://app.n.io/design.
1. Click the **add new system** card on the screen.
1. Complete the **create new system** modal:
  1. In the **system name** box, enter a name for your system.
  <img class="right border" src="/img/cloud/Hello-CreateNewSystem.gif" width="250" />
  2. In the **template** dropdown, you can keep the default blank system or select a system template.
  1. Click **accept**.

  ## {#pk-credentials}

  Your system has just spun up with a nio-managed [**Pubkeeper**](/pubkeeper) server. Pubkeeper is the network communications broker that enables elements in a nio system (other nio instances, UIs, or non-nio applications that use the Pubkeeper client) to talk to each other directly and securely.

  > **[info] <span class="allow-caps">Pubkeeper</span> server credentials**
  >
  > <img class="right border" src="/img/cloud/editSystem.png" width="250" />
  > To access your **Pubkeeper** credentials:
  > 1. In the app switcher on the left side of the System Designer, click the **design** app icon.
  > 1. You can see the configuration of the cloud Pubkeeper server if you hover over a system card and click the **edit** icon in the toolbar.
  > <br>
  > <br>

---

## Create a nio-managed cloud instance

<img class="right shadow" src="/img/cloud/addInstanceButton.png" width="200" />

A cloud instance is a running version of nio that is installed in the cloud and managed by niolabs.

1. From within your system, click **add instance** on the left side of the System Designer.
<img class="right border" src="/img/cloud/addInstance.png" width="250" />
1. Check the **cloud instance** checkbox if it is not checked automatically.
1. Complete the **add instance** window.
  1. In the **instance name** box, enter a name for your instance.
  1. Click **accept**.

<br>

Congratulations, you've set up a cloud instance!


---

## Now what?

If you are wondering how to use your cloud instance, head over to the workshops at [workshops.n.io](https://workshops.n.io)!

If you selected a system template, you should already have an instance (or two) pre-populated with some annotated services, ready for you to explore. See more information about system templates here: [workshops.n.io/system-templates](https://workshops.n.io/system-templates).
