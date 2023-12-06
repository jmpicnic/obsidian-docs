---
title: Building an Information Model
author: Miguel Pinilla
Copyright: (c) Miguel Pinilla, All rights reserved
License: "This work is licensed under the Creative Commons License CC BY-NC-SA 4.0: https://creativecommons.org/licenses/by-nc-sa/4.0/"
email: miguel.pinilla@saldubatech.com
share: "true"
---
## The Conceptual Model

The first step in building the information model for a system is to capture the concepts and relationships of the domain that the system will support. This requires collecting information, organizing them in a cohesive structure and document that structure to ensure that the different pieces fit together and to support future uses and team members.

### Collect Information

There are no magic shortcut to create the information model for a system, or modify an information model that already exists. It relies on a deep understanding of the domain and the requirements of the system. The sources to achieve this should not be a surprise to any practitioner:

* **Formal Requirements Documents**: Most organizations have some mechanism to capture the needs/requirements that the system needs to fulfill, they can be take the form of [*User Stories*](https://en.wikipedia.org/wiki/User_story), Structured [Use Cases](https://en.wikipedia.org/wiki/Use_case) , PRD documents, etc..
* **[Personas](https://en.wikipedia.org/wiki/Persona_(user_experience))**: If an organization keeps a library of Personas, they are a very valuable source of information about the expected *edge behaviors* of the system and what kind of experience users will find acceptable. Personas can also identify candidates for direct interviews and conversations to elicit information.
* **Existing Systems**: Most development projects involve improvements and changes to existing systems. Even if the functionality is completely new, the existing system or similar systems provide paradigms of use, information structure, etc...
* **Domain Experts**: should be at the top of the list for information gathering. Not only their explicit, codified knowledge, but paying attention to their language, the way they use terms and discuss problems is a rich source of domain concepts.
* **Academic/Scientific Literature**: There are very few fields that are so special or original that don't have some related studies done in academia. Although academic work may feel too removed from the reality of building a *real-world* system, there is no need, and it is always counter productive to reinvent concepts that may have been defined and distilled. This is obvious in some disciplines like life sciences, engineering or physics, and certain business domains like accounting. There are other disciplines like project management, business operations, etc... where this reinventing of the wheel happens too many times when there is a rich set of concepts in Operations Research, Organizational Behavior, etc. available.

### Organize Concepts

There are a number of brainstorming or ideation techniques that can be applied to finding concepts and their relationships when building Information Models. A few techniques are very productive in the early phases of discovery:

* **[Object Modeling in Color](https://en.wikipedia.org/wiki/Object_Modeling_in_Color)**. Which directs the attention of the team to discover the different kinds of concepts in the domain.
* **[Affinity Diagrams](https://asq.org/quality-resources/affinity)** that help collect concepts, create categories, identify duplicates, etc.
* **[Class, Responsibility and Collaboration](https://wwwcgi.teach.cs.toronto.edu/~csc207h/winter/lectures/L0201/w5/CRC.pdf)** To distill early concepts into classes and their relationships.
* **[Semantic Networks](https://en.wikipedia.org/wiki/Semantic_network) and [Semantic Fields](https://en.wikipedia.org/wiki/Semantic_field)**: To discover and document the structure of relationships between concepts.

By going through these activities, a team will naturally achieve the goal of a shared understanding of the domain. 

### Document the Domain

Documenting the results of the information model achieves two critical purposes. The obvious one is to enable those who will become part of the team in the future to join into that shared understanding without requiring a complete redo of the discovery process. The second one is to honor Einsteins statement that *[you do not really understand something unless you can explain it to your grandmother](https://www.goodreads.com/quotes/271951-you-do-not-really-understand-something-unless-you-can-explain)*. Documenting a design, and having it peer reviewed by the team is a guarantee that the design is understood and sound. 

The level of detail of the documentation will depend on the size and maturity of the team/organization, the complexity of the domain and also external requirements for regulated fields (e.g. requirements of design auditability in health care, energy or defense domains). Each organization needs to decide what level is the right one for them. The three essential types of documents to consider are:

1. A Glossary/Dictionary of all the concepts (nouns and verbs) identified, ideally with references to sources and examples of use.
2. A set of [class diagrams](Software%20Models.md#Class%20Models) class diagrams and associated descriptions for the main concepts. Diagrams should be centered around connected [classification hierarchies](Describing%20System%20State.md#Categorization%20and%20Classification). The level of detail and formalism may vary from simply providing the name of the class/interface to an almost programming language complete definition of a class (minus implementation)
3. [State Charts](Software%20Models.md#State%20Charts) for the central classes that govern the behavior of the system.

## Introduce Storage Considerations

With the steps given so far, the team can expect to gain a solid understanding of the domain and the content of the state of the system. This is not enough to guide the development of the system. At this point, the information model needs to be reconciled with the proposed deployment structure and the implementation technologies available to the development team.

### Partitioned Storage

Real world systems rarely have the luxury of being able to have a single, *flat* memory space for all its state. As discussed in [[Software Models]], physical limitations and requirements on location of data, lifecycles, etc. dictate that the state of the system will be partitioned in multiple storage systems. The information model resulting from the conceptual model needs to be enriched by defining what parts of it will be supported in each partition and how relationships between entities that end up in separate partitions will be implemented and maintained. Entities in the conceptual model need to be augmented with:

- Identities that include the address of their *home* storage so that they can be referred to unequivocally. The *home* storage is the one that is usually considered the *source of truth*, or the *data authority* that maintains that part of the state of the system.
- Complete or partial copies of the information contents of the entity in different storage areas to improve performance, reliability, access, etc...
- Synchronizations mechanisms to keep the copies consistent, at least with *[eventual consistency ](https://en.wikipedia.org/wiki/Eventual_consistency)* semantics, and associated mechanisms at the system level for error correction and to preserve functionality in the event of inconsistencies (E.g. *[Saga patterns](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/saga/saga)* and similar).

### Storage Technologies

Modeling complex domains benefit from the use of rich and expressive modeling frameworks like UML and other OO technologies that include capabilities that storage technologies don't support directly like inheritance, polymorphic identities/behaviors and others. The resulting conceptual model needs to be mapped onto the actual capabilities of the selected technology capabilities. In this section we will give an overview of these mappings leaving specific details for dedicated technology articles

#### Relational Storage

Relational mappings of Object Oriented models are well known due to the popularity of Object Relational Mapping tools like [Hibernate](https://hibernate.org/orm/faq/) these tools solve the following aspects of the *Object-Relational Impedance mismatch*:

- Flattening inheritance hierarchies into a single table, one table per concrete class with a discriminator table or separate tables.
- Flattening nested data structures to multiple columns of simple SQL types
- Represent 1:1, n:1 or 1:n associations through foreign keys, potentially multiple of them that can be nullified.
- Represent m:n associations through intersections tables

None of these techniques address relationships with entities in separate storage areas that are not reachable through the associated SQL query engine and need to be handled separately.

#### Document Storage

Document storage systems are able to represent complex nested data structures with limited capabilities to handle references between documents. Also, document databases are frequently *schemaless*, meaning that they can work with polymorphic data. The main design challenge is to overcome the relative inefficiency of retrieving information across multiple instances like selecting orders based on attribute values that belong to the buyer or seller. The information involved in these use cases needs to be replicated and embedded into the orders data storage and incur the cost of maintaining this denormalization.

#### Key-Value stores or Columnar Stores

These storage technologies can be similar to document storage when they can store complex data structures (e.g. by storing JSON objects). These technologies have reduced capabilities of using property values for business use cases (e.g. filtered queries) and don't usually support representation or traversal of associations. Complex domain models may require duplication of records in this kind of storage to support lookup based on different properties, either of the entity in question or associated entities.

### API Endpoints

Even in the cases where the state storage is mostly monolithic (e.g. a big backend RDBMS), modern systems offer their functionality through a set of API endpoints which are the ones that provide access to the system's observable state. The conceptual model needs to be expressed in terms of those API endpoints in a consistent way. Three aspects need to be explicitly designed to do this:

- Identities across API Endpoints. Entity instances will need to be addressed through the API endpoints and need to be identifiable within their *home* endpoint. An entity reference will then need to include (or be able to resolve) the API endpoint address, the protocol to use and a local identifier, very much similar to how REST identifies resources.
- Serialization of the Information Model Graph: The conceptual information model describes relationships between entities that may be *many-to-many*, cyclic or very deep in the relationship graph. When retrieving an entity from an API endpoint, the designer needs to strike a balance between the amount of information to serialize and include in the response and forcing the client to make multiple calls to the API endpoint (or different endpoints) to retrieve the information required. This decision must be driven by the expected use cases (e.g. presenting a summary list vs. details, avoiding common $n+1$ query patterns, etc.)
- Define specialized projections of entity information for common use cases which may include parts of multiple *fundamental* entities into a synthetic entity for the use case.

## Other Non Functional Considerations

In the process of defining the [conceptual model](/#The%20Conceptual%Model) of the domain, it is convenient to ignore certain non-functional considerations to focus on understanding the domain itself. Once this model is built, it is necessary to re-introduce those considerations to provide guidance to implementation, as some decisions need to be made with a broader scope than what specific implementation tasks would allow for. These decisions can be expressed as Stereotypes in UML if they correspond to well understood patterns (e.g. a requirement for an entity or a group of entities to be replicated in multiple independent storage capabilities, or directly described in the document. It cannot be over emphasized that any effort put into documentation must support the goal of creating a shared understanding of the system by the team to avoid over documenting and wasted effort.

Aspects to consider include:

- **Reliability/Fault Tolerance**: Determine what parts of the state need to be replicated in multiple storage capabilities, what is the tolerance for delays in synchronization/liveliness of replicated data and what kind of fault tolerance will be implemented (active/passive, active/active, number of replicas, recovery latency, ...)
- **Survivability**: What kind of incidents particular parts of the state need to be able to survive without interruption of service or with a limited time to recover. Part of the state may be O.K. if it does not survive a system restart, a session interruption, etc.. up to major disruptions of the supporting infrastructure (single zone or multi zone failures, storage corruption, ...)
- **Security and Access**: Whether parts of the model have additional requirements of isolation (e.g. Split a *User* entity into public and sensitive entities to comply with privacy regulations) or encryption, and what constraints (e.g. querying functionality) isolation or encryption pose.
- **Auditability**: Auditability requirements may be simply to maintain a textual log of the API operations on the system, or can be more complex requiring online inspection and analysis of detailed updates to individual entities. In the latter cases, the Information model may need to be augmented with records of updates and the provenance of those updates (i.e. user, interface used, date-time, authority, ...).
- **Journalling**: Some systems that are the source of truth for decisions and actions, need to be able to answer queries about the state of the system with respect to the time when an update was made to the system (i.e. *recorded at time*), as well as the time when the change was effective in the real world (i.e. business effective time). This kind of system requires entities to be *Versioned* in the system, with an information model that resembles the [event sourcing pattern](https://learn.microsoft.com/en-us/azure/architecture/patterns/event-sourcing)
- **Idempotency**: If part of the state needs to support idempotency w.r.t. repeated updates, it may need to be modeled with special requirements for how to identify instances and resolve equality. When considered in combination with Auditability and Journalling, Idempotency needs to specify the behavior of repeated updates. E.g. An idempotent update may result in a timestamped confirmation of a value, considered only in an audit log or ignored altogether.