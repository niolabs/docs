# Base Block Pattern

Implementing a base block pattern is useful in complex configurable blocks. In this pattern, configure the options that are not block-specific in a non-discoverable base block. The blocks that do the work and process signals will inherit from the base block.

For example, in a block that accesses an external API, you can use a base block to set up the base URL, and then create discoverable blocks to access each specific endpoint in the API. A base block pattern is easier to maintain and reinforces the "one function per block" philosophy.
