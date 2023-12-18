---
title: Impractical Architecture - System State
author: Miguel Pinilla
Copyright: (c) Miguel Pinilla, All rights reserved
License: "This work is licensed under the Creative Commons License CC BY-NC-SA 4.0: https://creativecommons.org/licenses/by-nc-sa/4.0/"
email: miguel.pinilla@saldubatech.com
share: "true"
---
This article is part of the series on [Impractical Domain Driven Development](https://medium.com/salduba/impractical-domain-driven-development-b9af36b0ede1) focusing on the creation of the information model of the system as part of architectural design activities. The framework article describes the information model:

> **Information Model**: What does the system keep as its internal state during and between activities and the structure of this state in smaller, well defined data structures.

The role of the information model in a computing system is to be able to describe the state of the system in a way that a development team, and possibly external stakeholders can understand the information it stores and then how the system uses it to respond to inputs and affect its environment.

## What is *State*

In following the impractical approach of the series, we will anchor the concept of *State* onto solid first principles, when talking about something as fuzzy as *state*, it is actually useful to go back to Turing's own formulation [Turing Machines.](https://plato.stanford.edu/entries/turing-machine/) In the original formulation the *state* state of the machine is simply an identifier of one of a finite number of possible states. In any binary (or discrete in general) system, this does not pose any constraints, one just needs to add more bits to the representation of the state to make it as granular as needed. So, at the bottom of it all the state is just a big binary number. Clearly this is not a reasonable answer for any real world system because of a couple of fundamental issues:

1. Systems need to be built, operated and maintained by people, so the state, together with the rest of the system needs to be understandable, and people are very bad at understanding unstructured bit fields of bits.

2. Regardless of [Moore's law](https://en.wikipedia.org/wiki/Moore%27s_law), performance limits of real computing, memory and communications hardware require the state to be partitioned, replicated, cached, etc..

To address these obstacles, we need to dig a bit deeper into how state is handled in computing systems by looking at their lifespan, the physical topology of storage and the technologies available to represent state.

The lifespan of specifics part of the state may be:

- Tied to the processing of a single input or request. In traditional programming languages this state is commonly kept in the "call stack" of the program. Usually this state can be purely "local" to the processing element.

- Used as "context" for a set of inputs or requests that occur in a reasonably short time interval. This context takes the form of "session" parameters in web applications, processing windows in event processing or data blocks in batch processing.

- Operational state that is modified/updated in the normal course of use of the system and it is expected to survive system restarts and other operational incidences. File systems, databases (in memory or permanent storage), etc... are commonly used to store and manage this state. Parts of this state may also have multiple replicas in the system for redundancy, performance, etc. which need to be synchronized.

- Configuration state, which is similar in implementation to the Operational State, but not usually updated during normal use of the system. Configuration state is updated only when the behavior of the system needs to change. Changes to the configuration state may involve system restarts or upgrades.

For each of these tiers, there are tradeoffs to be made between access speed, storage capacity and cost, which lead to the selection of different technologies for the different tiers.

It is very unusual to deal with a single storage space for the complete state. Even in small applications, storage is structured into some form of working stack, a global memory heap and some form of persistent storage, which in the simplest applications can just be a flat file in the operating system. Current applications and systems are much larger and increasingly subject to non functional requirements like jurisdictional data residency, privacy and security etc. As systems grow in complexity, so does the sophistication of the storage systems available to keep state, including:

- Working "stack" and "heap" memory in a thread or process. 
- Local and remote (network) file systems. 
- Databases using their own structure and access mechanisms. E.g. SQL databases partition the storage available to the application into databases, schemas, tables, rows and columns while internally using their own storage structures to optimize performance and scalability.
- Web or API based storage services with their own API's and structures.

The takeaway from this discussion is that in any real system state will be partitioned and the architecture and design of the system must explicitly address how to split the state and select the right technologies and storage topologies for the system. Fortunately, for broad classes of systems, design patterns have emerged that provide a good default recipe for the architecture, sometimes embodied in programming frameworks like [Ruby on Rails](https://rubyonrails.org/) or the [Java Platform, Enterprise Edition (Java EE) \| Oracle Technology Network](https://www.oracle.com/java/technologies/java-ee-glance.html). The downside of these patterns and frameworks is that they get ingrained in the practices of development teams and end up being applied "by-default" to systems that don't fit them (e.g. µ-services environments), frequently with disastrous results.

If the design of a system needs to address how state will be kept and managed, and even more importantly, understanding the state of the system is critical for a development, we need a solid set of practices and tools to express it.
