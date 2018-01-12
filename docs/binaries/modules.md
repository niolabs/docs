# Modules

Unlike a nio core component that runs only once in the core/main process, a nio module is a piece of functionality that runs in every nio service. Each nio module is broken down into two parts, an interface and an implementation.

---

## Interface
The interface of a module exists in the [block development framework](/blocks/block-development/framework.html) and can be called by the nio core or by blocks. This allows blocks to use the same implementation that the core uses in a particular installation without having to worry about the details of the implementation.

For example, rather than a block needing to define its own communication module, it can publish data using the same communication module interface that the core uses. This allows you to swap out the implementation of a service's communication without having to update all of your block code.

There are currently six module interfaces defined in the framework:
* Communication
* Scheduler
* Web Handler
* Persistence
* Security
* Settings

---

## Implementation

The other half of a module is the implementation, which defines how a module interface works. If the interface is how the module looks, the implementation is how it works.

Each nio binary will include one and only one implementation for each interface listed above. There is no way to include multiple implementations for a given binary. In order to run multiple implementations of a module interface you will need to run a new nio instance with a different binary.

Every nio service initializes all of its modules when it starts up. This means that module implementation code is run in every service process.
