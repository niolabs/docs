# Glossary of Terms

## Binary
A binary is the executable program that you run to run {{ book.product }}. Depending on your circumstances, you will run one of many {{ book.product }} binaries. Binaries range in complexity and are often tuned for particular hardware. If you're tinkering around on a Raspberry Pi, you don't need to run the same binary as a network of a dozen supercomputers built to analyze hundreds of thousands signals per second.

## Block
A block is a class that is built off of the Block Development Framework that defines methods to operate on streams of data. A block receives, emits, and/or transforms signals. Blocks are written in Python and tend to focus on one particular function. Blocks are reusable in any other services so it is beneficial to keep them modular.

## Framework
The Block Development Framework is the layered structure that defines how to develop blocks. This {{ book.product }} framework consists of the agreed upon interfaces that blocks and binaries understand. Install the framework with pip: `pip install nio`.

## Instance
A running version of the {{ book.product }} back end platform. Each host in a system will likely have at least one {{ book.product }} instance running on it.

## Project
A {{ book.product }} project is stored in a directory on your computer that contains the configuration that defines your {{ book.product }} implementation. Projects can run on their own or can be a part of a larger {{ book.product }} network where many instances communicate with one another.

## Pubkeeper
Pubkeeper™ is a communications broker that enables real-time data transfer between a system of disparate devices through standard publish-subscribe patterns. With Pubkeeper, two devices can interact with each other even if they do not sure the same communication protocol.

## Service
A service is a real-time process that runs on an instance. The logic is configured as a workflow of blocks. Services can be started and stopped.

## Signal
A signal is a unit of data that is passed from block to block within a service or between services. You can think of it as a little box of data, containing any data from a temperature reading to a tweet. It is internally represented as a key-value store.

## System
A system is a distributed set of entities that work together as a whole. For {{ book.product }}, this means a collection of {{ book.product }} back end instances and front end user interfaces that can communicate with one another in real time.
