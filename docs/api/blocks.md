# Blocks API #

Configured instances of a n.io block type are simply referred to as blocks. Earlier we saw an example of a Logger block instance created with the name ``Log``. Information and interaction with the block configurations of a running n.io instance is available through the blocks API.

## Get API ##

The get API returns a json body with information about a block based on its name. The following example gets the information for the configured Logger block ``Log``:

    curl -XGET 'http://localhost:8181/blocks/Log' --user 'Admin:Admin'

The result of the previous request is:

<dl>
  <dt>    {</dt>
  <dd>
    <p>{</p>
    <p>"type": "Logger",</p>
    <p>"name": "Log"</p>
    <p>"version": "0.0.0",</p>
    <p>"log_level": "INFO",</p>
    <p>"log_at": "INFO",</p>
    <p>}</p>
  </dd>
</dl>
<dl>
  <dt>type</dt>
  <dd>The block type of the block configuration.</dd>
</dl>
<dl>
  <dt>version</dt>
  <dd>The version of the block type when the block configuration was created.</dd>
</dl>
<dl>
  <dt>name</dt>
  <dd>The name of the block configuration. This must be unique among all blocks, regardless of type.</dd>
</dl>
<dl>
  <dt>log_level</dt>
  <dd>Level at which the block logs messages. Messages are logged for the specified ``log_level`` and all higher level.</dd>
</dl>
<dl>
  <dt>log_at</dt>
  <dd>``log_at`` is specific to the ``Logger`` block. It is the level at which Signal enter the block will be logged at. ``log_level`` needs to be at least ``log_at`` or lower for the Signals ot be logged.</dd>
</dl>
Each block type has its own unique properties that will be viewable here.

## Get All API ##

In addition to getting the details of one block configuration, specified by name, you can get the details of all block configurations in one request:

    curl -XGET 'http://localhost:8181/blocks' --user 'Admin:Admin'

## Create API ##

If you're working with a n.io project from scrach, you're going to be creating and configuring blocks. Create a new configuration of a block with the create API by POSTing JSON data. When creating a new block configuration, you can optionally include the configured values of the block type properties. At a minimum, you must specify the block ``type``, the ``name`` of the new configuration and values for any required properties that do not have a default value. For example, to create the ``Log`` block of type ``Logger``:

    curl -XPOST 'http://localhost:8181/blocks' --user 'Admin:Admin' --data '{"type": "LoggerBlock", "name": "Log"}' -H 'Content-Type: applcation/json'

## Update API ##

When you want to update the configuration of a block configuration, PUT the json data to the block name. You only need to PUT the properties that you are updating:

    curl -XPUT 'http://localhost:8181/blocks/Log' --user 'Admin:Admin' --data '{"log_level": "DEBUG"}' -H 'Content-Type: application/json'

## Delete API ##

Naturally, you'll make mistakes or refactor and want to delete a configured block:

    curl -XDELETE 'http://localhost:8181/blocks/Log' --user 'Admin:Admin'
