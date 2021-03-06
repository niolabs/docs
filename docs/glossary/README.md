# Glossary of terms

---

## Binary
A binary is the executable program that runs the nio Platform. Depending on your circumstances, you will run one of many nio binaries. Binaries range in complexity and are often tuned for particular hardware. If you're tinkering around on a Raspberry Pi, you don't need to run the same binary as a network of a dozen supercomputers built to analyze hundreds of thousands signals per second.

---

## Block
A block is a class that defines methods to operate on streams of data. A block receives, emits, and/or transforms signals. Blocks are written in Python and tend to focus on one particular function. Blocks are reusable in services so it is beneficial to keep them modular.

---

## Framework
The block development framework is the layered structure that defines how to develop blocks. This nio framework consists of the agreed upon interfaces that blocks and binaries understand. Install the framework with pip: `pip install nio`.

---

## Instance
A running version of the nio Platform. Each host in a system will likely have at least one nio instance running on it.

---

## Project
A nio project is stored in a directory on your computer and contains the configuration that defines your nio implementation. Projects can run on their own or can be a part of a larger nio network where many instances communicate with one another.

---

## <span class="allow-caps">Pubkeeper</span>
Pubkeeper is a communications broker that enables real-time data transfer between a system of disparate devices through standard publish-subscribe patterns. With Pubkeeper, two devices can interact with each other even if they do not share the same communication protocol.

---

## Service
A service is a real-time process that runs on an instance. The logic is configured as a workflow of blocks. Services can be started and stopped.

---

## Signal
A signal is a unit of data that is passed from block to block within a service or between services. You can think of it as a little package of data, containing any data from a temperature reading to a tweet. It is internally represented as a key-value store.

---

## System
A system is a distributed set of entities that work together as a whole. For nio, this means a collection of nio back end instances and front end user interfaces that can communicate with one another in real time.
