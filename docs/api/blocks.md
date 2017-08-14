# Blocks API

A configured instance of a {{ book.product }} block type is referred to simply as a block. While block types are classes and have code, blocks are specific configurations of a block type's properties. Earlier we saw an example of a _Logger_ block instance created with the name `Log`. Information about and interaction with individual block configurations in a running {{ book.product }} instance are available through the `/blocks` API.  

## Get API

The Get API returns a JSON body with information about a block based on its name. The following example gets the information for the configured _Logger_ block with the name `Log`

    curl -XGET 'http://localhost:8181/blocks/Log'

The result of the previous request is

```json
{
  "type": "Logger",
  "version": "1.0.0",
  "name": "Log",
  "log_level": "INFO",
  "log_at": "INFO"
}
```
The following four properties are common to all block types:

**type**<br>The block type of the block configuration.

**version**<br>The version of the block when the block configuration was created.

**name**<br>The name of the block configuration. This must be unique among all blocks, regardless of type.

**log_level**<br>The number of log messages displayed, from `NOTSET` on the bottom, which includes all messages logged, to `CRITICAL` on the top, which contains only the most critical messages. Messages are shown for the specified `log_level` and all levels above.

Other properties are block type-specific: 

**log_at**<br>`log_at` is a property specific to the _Logger_ block type and is detailed in the _Logger_ block type specifications.

Other block types will show their own properties in the response. For example, the _AttributeSelector_ block type has an `attributes` property instead of 'log_at'.

      "attributes": []

## Get All API

In addition to getting the details of one block configuration, specified by name, you can get the details of all block configurations in one request

    curl -XGET 'http://localhost:8181/blocks'

## Create API

If you're working with a {{ book.product }} project from scratch, you need to create and configure blocks. You can create a new configuration of a block with the Create API by sending a POST request to `/blocks` with the applicable JSON data. When creating a new block configuration, optionally you can include the configured values of the block type's properties. At a minimum, you must specify the block `type`, the `name` of the new configuration, and values for any required properties that do not have a default value. For example, to create a _Logger_ block type with the name `Log`

    curl -XPOST 'http://localhost:8181/blocks' --data '{"type": "LoggerBlock", "name": "Log"}' -H 'Content-Type: application/json'

## Update API

When you want to update the configuration of a block, send a PUT request to `/blocks` with the block-name endpoint and include the new JSON data. You only need to include the properties that you are updating in your PUT request, in this case `log_level`.

    curl -XPUT 'http://localhost:8181/blocks/Log' --data '{"log_level": "DEBUG"}' -H 'Content-Type: application/json'

## Delete API

To delete a named block, send a DELETE request to `/blocks` with the name of the block you want to delete as the endpoint.

    curl -XDELETE 'http://localhost:8181/blocks/Log'
