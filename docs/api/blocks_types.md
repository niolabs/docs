# Blocks Types API

{{ book.product }} block types are the functional pieces of code that generate signals and/or do work with them. Earlier we saw examples of block types such as _CounterIntervalSimulator_ and _Logger_. Information about and interaction with the blocks of a running {{ book.product }} instance are available through the `/blocks_types` API.

## Get API

A `GET` request sent to the `/blocks_types/<block type name>` endpoint will return a JSON body with information about that block type.

The following example gets the information for the _Logger_ block type

    curl -XGET 'http://localhost:8181/blocks_types/Logger'

The result of the previous request is
```json
{
  "name": "Logger",
  "version": "0.0.0",
  "namespace": "blocks.logger.logger_block.Logger",
  "properties": {
    "type": {
      "allow_none": false,
      "title": "Type",
      "default": null,
      "type": "StringType",
      "visible": false,
      "readonly": true
    },
    "version": {
      "type": "StringType",
      "allow_none": false,
      "visible": true,
      "title": "Version",
      "default": "0.0.0"
    },
    "log_level": {
      "allow_none": false,
      "options": {
        "ERROR": 40,
        "DEBUG": 10,
        "INFO": 20,
        "WARNING": 30,
        "NOTSET": 0,
        "CRITICAL": 50
      },
      "title": "Log Level",
      "enum": "LogLevel",
      "type": "SelectType",
      "default": "INFO",
      "visible": true
    },
    "log_at": {
      "allow_none": false,
      "options": {
        "ERROR": 40,
        "DEBUG": 10,
        "INFO": 20,
        "WARNING": 30,
        "NOTSET": 0,
        "CRITICAL": 50
      },
      "title": "Log At",
      "enum": "LogLevel",
      "type": "SelectType",
      "default": "INFO",
      "visible": true
    },
    "name": {
      "type": "StringType",
      "allow_none": false,
      "visible": false,
      "title": "Name",
      "default": null
    }
  },
  "commands": {
    "properties": {
      "title": "properties",
      "params": {}
    },
    "log": {
      "title": "log",
      "params": {
        "phrase": {
          "allow_none": false,
          "title": "phrase",
          "default": "Default phrase"
        }
      }
    }
  },
  "attributes": {
    "output": [
      {
        "id": "__default_terminal_value",
        "label": "default",
        "order": 0,
        "default": true,
        "type": "output",
        "description": "",
        "visible": true
      }
    ],
    "input": [
      {
        "id": "__default_terminal_value",
        "label": "default",
        "order": 0,
        "default": true,
        "type": "input",
        "description": "",
        "visible": true
      }
    ]
  },
}
```

**name**<br>The name of the block type.

**version**<br>The version of the block type that is being used by the running {{ book.product }} instance.

**namespace**<br>The class the block type is imported from.

**properties**<br>Each of the block's configurable attributes and information about them, including
 - **type**<br>The property type.
 - **name**<br>The block name.
 - **default**<br>The default value.
 - **title**<br>The title that will display in the block configuration panel.
 - **allow_none**<br>True if the property configuration is optional, false if required.
 - **visible**<br>True if the property shows up in the configuration panel, false if does not appear.

**commands**<br>Executable commands on running blocks and all information about them, including
  - **title**<br>The name of the command.
  - **params**<br>Any parameters the command method takes.

**attributes**<br>Any additional block attributes, including
  - **input**<br>The input terminal(s) for incoming signals.
  - **output**<br>The output terminal(s) for outgoing signals.

## Get All API

In addition to getting the details of one block type, specified by name, you can get the details of all of your project's block types in one request.

    curl -XGET 'http://localhost:8181/blocks_types'

## Add API

When {{ book.product }} starts up, it discovers and adds all the block types in the project. If you add a new block type to a running instance of {{ book.product }}, it will not be discovered until nio starts again. However, you can add the new block type to a running instance with the Add API. After the block code is added to the project directory, send a PUT request to the new block type name to load the new block type into the running {{ book.product }} instance

    curl -XPUT 'http://localhost:8181/blocks_types/<NewBlockTypeName>'

## Update API

When {{ book.product }} starts up, it discovers and adds all the block types in the project. When code in an existing block type is changed in a project (usually after upgrading to a newer version of the block type) in a running {{ book.product }} instance, the running {{ book.product }} instance needs to be told to use that updated code. You can do that with the Update API. Once the new block code is updated in the project directory, send a PUT request to the updated block type to load it into the running {{ book.product }} instance

    curl -XPUT 'http://localhost:8181/blocks_types/Logger'
