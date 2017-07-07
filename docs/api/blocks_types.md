# Blocks Types API #

n.io blocks are the functional pieces of code that generate signals and/or do work with them. Earlier we saw examples of blocks such as CounterIntervalSimulator and Logger. Information and interaction with the blocks of a running n.io instance is available through the blocks types API.

## Get API ##

The get API return a json body with information about a block type based on its name. The following example gets the information for the Logger block:

    curl -XGET 'http://localhost:8181/blocks_types/Logger' --user 'Admin:Admin'

The result of the previous request is:

<dl>
  <dt>    {</dt>
  <dd>
    <p>{</p>
    <p>"name": "Logger",</p>
    <p>"version": "0.0.0",</p>
    <p>"namespace": "blocks.logger.logger_block.Logger",</p>
    <p>"properties": {</p>
    <p>"log_level": {</p>
    <p>"enum": "LogLevel",</p>
    <p>"allow_none": false,</p>
    <p>"options": {</p>
    <p>"CRITICAL": 50,</p>
    <p>"INFO": 20,</p>
    <p>"NOTSET": 0,</p>
    <p>"ERROR": 40,</p>
    <p>"WARNING": 30,</p>
    <p>"DEBUG": 10</p>
    <p>},</p>
    <p>"type": "SelectType",</p>
    <p>"default": "INFO",</p>
    <p>"visible": true,</p>
    <p>"title": "Log Level"</p>
    <p>},</p>
    <p>"name": {</p>
    <p>"allow_none": false,</p>
    <p>"default": null,</p>
    <p>"visible": false,</p>
    <p>"title": "Name",</p>
    <p>"type": "StringType"</p>
    <p>},</p>
    <p>"log_at": {</p>
    <p>"enum": "LogLevel",</p>
    <p>"allow_none": false,</p>
    <p>"options": {</p>
    <p>"CRITICAL": 50,</p>
    <p>"INFO": 20,</p>
    <p>"NOTSET": 0,</p>
    <p>"ERROR": 40,</p>
    <p>"WARNING": 30,</p>
    <p>"DEBUG": 10</p>
    <p>},</p>
    <p>"type": "SelectType",</p>
    <p>"default": "INFO",</p>
    <p>"visible": true,</p>
    <p>"title": "Log At"</p>
    <p>},</p>
    <p>"type": {</p>
    <p>"allow_none": false,</p>
    <p>"type": "StringType",</p>
    <p>"default": null,</p>
    <p>"readonly": true,</p>
    <p>"visible": false,</p>
    <p>"title": "Type"</p>
    <p>},</p>
    <p>"version": {</p>
    <p>"allow_none": false,</p>
    <p>"default": "0.0.0",</p>
    <p>"visible": true,</p>
    <p>"title": "Version",</p>
    <p>"type": "StringType"</p>
    <p>}</p>
    <p>},</p>
    <p>"commands": {</p>
    <p>"properties": {</p>
    <p>"params": {},</p>
    <p>"title": "properties"</p>
    <p>},</p>
    <p>"log": {</p>
    <p>"params": {</p>
    <p>"phrase": {</p>
    <p>"default": "Default phrase",</p>
    <p>"allow_none": false,</p>
    <p>"title": "phrase"</p>
    <p>}</p>
    <p>},</p>
    <p>"title": "log"</p>
    <p>}</p>
    <p>},</p>
    <p>"attributes": {</p>
    <p>"output": [</p>
    <p>{</p>
    <p>"label": "default",</p>
    <p>"visible": true,</p>
    <p>"id": "__default_terminal_value",</p>
    <p>"type": "output",</p>
    <p>"default": true,</p>
    <p>"order": 0,</p>
    <p>"description": ""</p>
    <p>}</p>
    <p>],</p>
    <p>"input": [</p>
    <p>{</p>
    <p>"label": "default",</p>
    <p>"visible": true,</p>
    <p>"id": "__default_terminal_value",</p>
    <p>"type": "input",</p>
    <p>"default": true,</p>
    <p>"order": 0,</p>
    <p>"description": ""</p>
    <p>}</p>
    <p>]</p>
    <p>}</p>
    <p>}</p>
  </dd>
</dl>
<dl>
  <dt>name</dt>
  <dd>The name of the block type.</dd>
</dl>
<dl>
  <dt>version</dt>
  <dd>The version of the block type that is being used by the running n.io instance.</dd>
</dl>
<dl>
  <dt>namespace</dt>
  <dd>Where the block type is imported from.</dd>
</dl>
<dl>
  <dt>properties</dt>
  <dd>Each of the configurable block attributes and all information about them (i.e. property ``type``, ``name``, ``default`` value, display ``title``, if it can ``allow_none``, etc...).</dd>
</dl>
<dl>
  <dt>commands</dt>
  <dd>Executable commands on running blocks and all information about them (i.e. command ``title`` and ``params``).</dd>
</dl>
<dl>
  <dt>attributes</dt>
  <dd>Any additional block attributes, including Signal ``input`` and ``output`` points.</dd>
</dl>
## Get All API ##

In addition to getting the details of one block type, specified by name, you can get the details of all blocks in one request:

    curl -XGET 'http://localhost:8181/blocks_types' --user 'Admin:Admin'

## Add API ##

When n.io starts up, it discovers and adds all the block types in the project. If you want to add a new block to an already runnning n.io instance, you can do that with the Add API. Once the block code is added to the project directory, use the following request to load it into the running n.io instance:

    curl -XPUT 'http://localhost:8181/blocks_types/Logger' --user 'Admin:Admin'

## Update API ##

When n.io starts up, it discovers and adds all the block types in the project. When block code is changed in a project (likely as a result of upgrading to a newer version of the block) to an already runnning n.io instance, the running n.io instance needs to be told to use that new updated code. You can do that with the Update API. Once the new block code is updated in the project directory, use the following request to load it into the running n.io instance:

    curl -XPUT 'http://localhost:8181/blocks_types/Logger' --user 'Admin:Admin'
