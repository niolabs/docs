# Glossary of Terms #

## System
A distributed set of entities that work together as a whole. For n.io, this means a collection of n.io backend instances and frontend user interfaces that can communicate with one another in real time.

## Instance
A running version of the n.io backend platform. Each host in a system will want (at least) one n.io instance running on it.

## Service
A real time process that runs on an instance. Its logic is configured as a workflow of blocks. Services can be started and stopped.

## Block
A “black box” function that operates on streams of data. Either receives signals, emits signals, or both. Blocks are written in Python and should focus on one particular function.

## Binary
Depending on your circumstances, you will run one of many n.io binaries. Binaries range in complexity and are often tuned for hardware. If you're tinkering around on a Raspberry Pi, you don't need to run the same binary as a network of a dozen super computers built to analyze hundreds of thousands signals per second.

## Framework
The n.io library is the versioned portion of the n.io code. You will install the n.io library and then execute that with the appropriate n.io binary. Install the framework with pip: `pip install nio`.

## Project
A n.io project is a directory on your computer that contains all the configuration that defines your n.io implementation. Projects can run stand-alone or they can be a part of a larger n.io network where many n.io instances communicate with one another.

## Signal
A signal is a unit of data that is passed from block to block within a service. Think of it is a little box of data, containing anything from a temperature reading to a tweet.
