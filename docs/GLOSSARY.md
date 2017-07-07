# Glossary of Terms #

## System
A distributed set of entities that work together as a whole. For n.io, this means a collection of n.io backend instances and frontend user interfaces that can communicate with one another in real time.

## Instance
A running version of the n.io backend platform. Each host in a system will want (at least) one n.io instance running on it.

## Service
A real time process that runs on an instance. Its logic is configured as a workflow of blocks. Services can be started and stopped.

## Block
A “black box” function that operates on streams of data. Either receives signals, emits signals, or both. Blocks are written in Python and should focus on one particular function.
