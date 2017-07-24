# Glossary of Terms

## Binary
A binary is the executable program. Depending on your circumstances, you will run one of many n.io binaries. Binaries range in complexity and are often tuned for particular hardware. If you're tinkering around on a Raspberry Pi, you don't need to run the same binary as a network of a dozen supercomputers built to analyze hundreds of thousands signals per second.

## Block
A block is a single function that operates on streams of data. A block receives, emits, or transforms signals. Blocks are written in Python and focus on one particular function.

## Framework
A framework is the layered structure of how n.io is built and how they interrlate. The n.io library is the versioned portion of the n.io code. You will install the n.io library and then execute that with the appropriate n.io binary. Install the framework with pip: `pip install nio`.

## Instance
A running version of the n.io back end platform. Each host in a system requires at least one n.io instance running on it.

## Project
A n.io project is stored in a directory on your computer that contains the configuration that defines your n.io implementation. Projects can run on their own or can be a part of a larger n.io network where many instances communicate with one another.

## Service
A service is a real-time process that runs on an instance. The logic is configured as a workflow of blocks. Services can be started and stopped.

## Signal
A signal is a unit of data that is passed from block to block within a service. You can think of it is a little box of data, containing any data from a temperature reading to a tweet.

## System
A system is a distributed set of entities that work together as a whole. For n.io, this means a collection of n.io back end instances and front end user interfaces that can communicate with one another in real time.
