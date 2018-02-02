# Organization management

<img class="right shadow" src="/img/organizations/org-account-settings.jpg" width="200"/>
To view your organization, hover over the user icon &nbsp;<img class="inline" src="/img/organizations/user-icon.png" height="20"/>&nbsp; in the top navigation  (on mobile, select **Settings** from the dropdown menu) and select your organization from the dropdown.

<br>
<br>
<br>
<br>
Each user in an organization can have one of three roles: owner, organizer, or collaborator.


---
## Owner
There is only one owner and the owner has complete administrative access to the organization. The owner role is limited to the person who originally set up the license.

The owner is able to invite users at two different permission levels: organizer or collaborator.

![](/img/organizations/org-inviteuser.jpg)

Each permission level comes with the following abilities:

| | Create Organizations | Create Teams | Add Users | Share Systems | Manage Plan |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| **Owner** | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) |
| **Organizer** | ![](/img/icons/times-red.svg) |  ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/times-red.svg) |
| **Collaborator** | ![](/img/icons/times-red.svg) | ![](/img/icons/times-red.svg) | ![](/img/icons/times-red.svg) | ![](/img/icons/times-red.svg) | ![](/img/icons/times-red.svg) |


---
## Organizer
Organizers can add users, create teams, and manage the permission levels of users and teams. The main difference between the owner and an organizer is that the owner has access to the billing information of the organization.

---
## Collaborator
Collaborators can view users and teams but are not be able to add users or manage teams. Collaborators can only see systems that have been shared with them in the nio System Designer.

When an owner or organizer shares a nio system with a collaborator or team, they must assign one of the three permissions:

* admin
* editor
* viewer

![](/img/organizations/org-share-viewer.jpg)

Each of these three levels of permissions allows a varying level of access within the nio System Designer.

### Sharing

Permission levels assigned to collaborators in the System Designer

| | system |
| ------------- | ------------- |
| **admin** | ![](/img/icons/checkmark-green.svg) |
| **editor** | ![](/img/icons/times-red.svg) |
| **viewer** | ![](/img/icons/times-red.svg) |

### Creating

Permission levels assigned to collaborators in the System Designer

| | system |instance | service | block |
| ------------- | ------------- |------------- |------------- |------------- |
| **admin** | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) |
| **editor** | ![](/img/icons/times-red.svg) | ![](/img/icons/times-red.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) |
| **viewer** | ![](/img/icons/times-red.svg) | ![](/img/icons/times-red.svg) | ![](/img/icons/times-red.svg) | ![](/img/icons/times-red.svg) |

### Editing

Permission levels assigned to collaborators in the System Designer

| | system |instance | service | block |
| ------------- | ------------- |------------- |------------- |------------- |
| **admin** | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) |
| **editor** | ![](/img/icons/times-red.svg) | ![](/img/icons/times-red.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) |
| **viewer** | ![](/img/icons/times-red.svg) | ![](/img/icons/times-red.svg) | ![](/img/icons/times-red.svg) | ![](/img/icons/times-red.svg) |


### Viewing

Permission levels assigned to collaborators in the System Designer

| | system |instance | service | block |
| ------------- | ------------- |------------- |------------- |------------- |
| **admin** | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) |
| **editor** | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) |
| **viewer** | ![](/img/icons/times-red.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) |


### Deleting

Users with **deleting** access can delete nio artifacts as shown in the table below. Editors can delete services and blocks but not systems or instances.

| | system |instance | service | block |
| ------------- | ------------- |------------- |------------- |------------- |
| **admin** | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) |
| **editor** | ![](/img/icons/times-red.svg) | ![](/img/icons/times-red.svg) | ![](/img/icons/checkmark-green.svg) | ![](/img/icons/checkmark-green.svg) |
| **viewer** | ![](/img/icons/times-red.svg) | ![](/img/icons/times-red.svg) | ![](/img/icons/times-red.svg) | ![](/img/icons/times-red.svg) |


### See who has access

Users with **see-who-has-access** privileges can see which systems another user has access to. As shown in the table below, only admins can see which systems another user has access to.

| | system |
| ------------- | ------------- |
| **admin** | ![](/img/icons/checkmark-green.svg) |
| **editor** | ![](/img/icons/times-red.svg) |
| **viewer** | ![](/img/icons/times-red.svg) |


### Revoking access

Users with **revoking-access** can revoke another user’s access to a system as shown in the table below. Only admins can revoke a user’s access to a system.

| | system |
| ------------- | ------------- |
| **admin** | ![](/img/icons/checkmark-green.svg) |
| **editor** | ![](/img/icons/times-red.svg) |
| **viewer** | ![](/img/icons/times-red.svg) |
