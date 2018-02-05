# nio-managed cloud instance

While the true power of the nio Platform is experienced when you have multiple [local installations](/running-nio/locally.html) communicating across a distributed network, we also offer the ability to spin up nio-managed cloud instances through the **nio System Designer**.

A nio-managed cloud instance allows you to get up and running quickly and to start building services right away (although our local installation process usually only takes 5 minutes!).

>**[info] Prerequisites**
>
>* **A nio account**: [Sign up here](https://app.n.io/signup)

---

## Create a system
<img class="right border" src="/img/cloud/Hello-CreateNewSystem.png" width="250" />

A system is a group of interrelated elements. In the nio System Designer, a system contains interrelated nio instances. Think of it as a workspace where you can put related projects.
1. Open the **System Designer**: https://designer.n.io/.
1. You can create a new system in two ways:
  * If this is your first time opening the System Designer, the **create new system** modal window displays automatically.
  * If it doesn't open automatically, click the **`+`** button in the lower-left corner of the System Designer.
1. Complete the **create new system** modal:
  1. In the **system name** box, enter a name for your system.
  1. Click **accept**.

---

## Create a nio-managed cloud instance

A cloud instance is a running version of nio that is installed in the cloud and managed by niolabs.

<img class="right border" src="/img/cloud/Hello-CreateCloudInstance.png" width="250" />

1. In your system's toolbar, click **create cloud instance**.
1. Complete the **create cloud instance** window.
  1. In the **instance name** box, enter a name for your instance.
  1. Click **accept**.

<br>
<br>

Congratulations, you've set up a cloud instance!

In addition to a running nio instance, we have also set up a nio-managed instance of [**Pubkeeper**](/pubkeeper). Pubkeeper is the network communication broker that enables elements in a nio system (other nio instances, UIs, or non-nio applications that use the Pubkeeper client) to talk to each other directly and securely.

To access your **Pubkeeper** credentials:
1. Click on your system's name on the left hand side of the System Designer.
1. Click the **edit** button in the contextual toolbar above the canvas.
1. Your **Pubkeeper** configuration details will be shown in the modal window.

---

## Now what?

If you are wondering how to use your cloud instance? Head over to the workshops at [workshops.n.io](https://workshops.n.io)!
