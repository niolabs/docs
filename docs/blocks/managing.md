# Managing your Blocks

The nio platform comes with a powerful mechanism to manage block installations and versions in your nio projects. Blocks can be saved locally in project folders or can be sourced from git repositories. The latter is more common as most of the common nio blocks are contained in individual git repositories.

An instance's block inventory is contained in the **etc/blocks.cfg** file.

## Adding a new block to an instance

### Using the CLI

To add a block to an instance using the nio CLI navigate to the project folder and run the following command:
```
nio add filter
```

This will add the filter block repository (containing the Filter block) to the project. This is using the nio block shorthand, available for blocks that exist in the [nio-blocks GitHub organization](https://github.com/nio-blocks).

To add a block from a git repository not in the nio-blocks organization provide the full git clone URL instead:
```
nio add git://github.com/nio-blocks/filter.git
```

### Using the API

You can also add blocks via the nio instance's REST API.

```
POST https://NIOHOST/project/blocks
{
  "url": "filter"
}
```

Similar to the CLI, you can also add blocks by their git clone URL if they don't exist in the nio-blocks GitHub organization.

```
POST https://NIOHOST/project/blocks
{
  "url": "git://github.com/nio-blocks/filter.git"
}
```

You can also add blocks from a specific git tag or branch by including that in the JSON body of the request
```
POST https://NIOHOST/project/blocks
{
  "url": "git://github.com/nio-blocks/filter.git",
  "branch": "master"
}
```
```
POST https://NIOHOST/project/blocks
{
  "url": "git://github.com/nio-blocks/filter.git",
  "tag": "v2.0.0"
}
```

## Updating a block

You can update a block to a new tag or branch by making requests to the nio API with the branch or tag to pull from. If you include a branch or tag in a block update request then they will be pulled from the git remote. If you do not include a branch or tag, then no git pull will occur.

```
PUT https://NIOHOST/project/blocks
{
  "url": "git://github.com/nio-blocks/filter.git",
  "branch": "master"
}
```

The previous HTTP request will pull the latest block code from the **master** branch. The branch will not be pulled again until a subsequent HTTP request is made or a deployment to the instance occurs.
