REST API
===============
How to use
----------
A great way to send / receive rest API calls is with the [Postman extension for Chrome](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0CCAQFjAA&url=https%3A%2F%2Fchrome.google.com%2Fwebstore%2Fdetail%2Fpostman-rest-client%2Ffdmmgilgnpjigdojojpjoooidkmcomcm%3Fhl%3Den&ei=xsk-VMWMOIakyQTdy4HoDw&usg=AFQjCNHaecLwAKk91gpdCY_y1x_ViIrHwQ&sig2=okzoFMhfnHVhLnA_BVuXDQ&bvm=bv.77412846,d.aWw)

- set the url to http://IP_ADDRESS:port/COMMAND
- set correctly to either GET, POST, PUT, or DELETE

Commands
----------
User authentication depends on the configuration of the nio project's security settings.

/nio
-------------------------

**GET**

Get nio version, component versions and module versions.

/blocks
--------------------

**GET**

Get all block configurations.

**POST**

Create a new block configuration.

Post body needs to include "type" and "name" where "type" is the block type and "name" is the name of your new block configuration.

/blocks/{{block_name}}
--------------------

**GET**

Get configuration of a block.

**PUT**

Update configuration of a block.

**DELETE**

Delete a block.

/blocks_types
--------------------

**GET**

Get block types that are loaded into the nio instance.

/services
--------------------

**GET**

Get all service configurations.

**POST**

Create a new service configuration.

Post body needs to include "type" and "name" where "type" is the serivce type (i.e. "Service") and "name" is the name of your new service configuration.

/services/{{service_name}}
--------------------

**GET**

Get configuration of a service.

**PUT**

Update configuration of a service.

**DELETE**

Delete a service.

/services/{{service_name}}/{{command_name}}
--------------------

**GET**

Execute a command on a service.

Built-in commands are *start*, *stop* and *status*.

/services/{{service_name}}/{{block_name}}/{{command_name}}
--------------------

**GET**

Execute a command on a running block inside a serivce.

/services_types
--------------------

**GET**

Get service types that are loaded into the nio instance.

/shutdown
-------------------------

**GET**

Shutdown the nio instance.
