# Blocks Types API

{{ book.product }} block types are the functional pieces of code that generate signals and/or do work with them. Earlier we saw examples of block types such as _CounterIntervalSimulator_ and _Logger_. Information about and interaction with the blocks of a running {{ book.product }} instance is available through the **blocks types** API.

## Get

A `GET` request sent to the `/block_types/<block type name>` endpoint will return a JSON body with information about that block type.

The following example gets the information for the _Logger_ block type:

    curl -XGET 'http://localhost:8181/blocks_types/Logger' -H 'authorization: Basic <your encrypted password>'

The result of the previous request is:
```json
{
  "name": "Logger"
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
      "params": {},
      "title": "properties"
    },
    "log": {
        "params": {
          "phrase": {
            "allow_none": false,
            "title": "phrase",
            "default": "Default phrase"
          }
        },
        "title": "log"
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
}```

**name**<br>The name of the block type.

**version**<br>The version of the block type that is being used by the running {{ book.product }} instance.

**namespace**<br>Where the block type is imported from.

**properties**<br>Each of the block's configurable attributes and all information about them, including
 - **type**<br>The property type.
 - **name**<br>The block name.
 - **default**<br>The default value.
 - **title**<br>The title that will display in the block configuration panel.
 - **allow_none**<br>Whether the property is optional.
 - **visible**<br>Whether the property shows up in the configuration panel.

**commands**<br>Executable commands on running blocks and all information about them, including
  - **title**<br>The name of the command.
  - **params**<br>Any parameters the command method takes.

**attributes**<br>Any additional block attributes, including
  - **input**<br>The signal input terminal(s).
  - **output**<br>The signal output terminal(s).

## Get All

In addition to getting the details of one block type, specified by name, you can get the details of all of your project's block types in one request

    curl -XGET 'http://localhost:8181/blocks_types' --user 'Admin:Admin'

## Add

When {{ book.product }} starts up, it discovers and adds all the block types in the project. If you add a block type to a running instance of {{ book.product }}, it will not be discovered until nio starts again. However, you can add the new block type to a running instance with the Add API. After the block code is added to the project directory, use the following request to load the new block type into the running {{ book.product }} instance:

    curl -XPUT 'http://localhost:8181/blocks_types/<NewBlockTypeName>' --user 'Admin:Admin'

## Update

When {{ book.product }} starts up, it discovers and adds all the block types in the project. When code in an existing block type is changed in a project (likely as a result of upgrading to a newer version of the block) in a running {{ book.product }} instance, the running {{ book.product }} instance needs to be told to use that new updated code. You can do that with the Update API. Once the new block code is updated in the project directory, use the following request to load the updated block into the running {{ book.product }} instance:

    curl -XPUT 'http://localhost:8181/blocks_types/Logger' --user 'Admin:Admin'
