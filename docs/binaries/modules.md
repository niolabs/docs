# Modules

A module is one of the three parts of a nio [binary](/binaries/README.md), along with the nio core and [components](/binaries/components.md). A module is broken down into two parts, an interface and an implementation.

The interface of a module exists in the [block development framework]() <!-- TODO: add correct link --> and can be called by the nio core or by blocks. This allows blocks to use the same implementation that the core uses in a particular installation without having to worry about that implementation.

For example, rather than a block having to define its own communication module, it can publish data using the agreed upon communication module interface. The core will use this same module interface. This allows us to swap out the implementation of how communication actually works without having to update all of our block code.

There are currently six module interfaces, all defined in the framework:
* Communication
* Scheduler
* Web Handler
* Persistence
* Security
* Settings

The other half of a module is the implementation, which defines how a module interface will work. If the interface is how the module looks, the implementation is how it works.

Each nio binary will include one and only one implementation for each module listed above. There is no way to include multiple implementations for a given binary. In order to run multiple implementations of a module interface you will need to run a new nio instance with a different binary.

Every nio service will first initialize every module when it starts up. This means that module implementation code is run in every service process. This differs from components which are described in the next section.
