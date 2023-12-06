---
title: Impractical Architecture - System State
author: Miguel Pinilla
Copyright: (c) Miguel Pinilla, All rights reserved
License: "This work is licensed under the Creative Commons License CC BY-NC-SA 4.0: https://creativecommons.org/licenses/by-nc-sa/4.0/"
email: miguel.pinilla@saldubatech.com
share: "true"
---
Describing the state of a system is at its core a problem of organizing and presenting information about the world. This is probably one of the oldest and most studied topics in history ever since Philosophy is practiced. There are a few tools coming from the field of [Ontology](https://en.wikipedia.org/wiki/Ontology) that are used everyday by engineers and architects, many times without even realizing, that are worth reviewing. When needing to describe a domain, we describe the object or entities that are in the domain, how we identify them, how they are similar or different, what attributes they have, how they are related to each other and what events and changes we can effect or observe in those objects. The conceptual tools to do this systematically are well understood.

## Identity

In any description of the objects of a domain, the ability to define whether two presented objects are the same or not is a critical consideration in modeling. THis may feel very abstract and theoretical, but it has direct implications for how we design databases with natural or synthetic keys, how to implement equality comparisons in code and whether we are dealing with "Pass by Value" or "Pass by reference" semantics in a system.

## Categorization and Classification

When presented with objects of the domain, we can group them in categories based on some criteria of similarity or equality. These categories may themselves be grouped in larger categories, resulting in a Classification, which can be purely hierarchical or form a graph-like structure.

## Decomposition and Properties

Objects in a domain can be described by providing descriptions of "parts" that together form it. Each part is itself subject to categorization and is a "property" of the object. Properties may take the form of a database column, an attribute of an object or a method that retrieves a value. The essential characteristic of a property is that it must be observable, that is that its value can be obtained from the object or the domain.

## Relations and References

A particular kind of "part" of an object may be a reference to another object that is not the object itself. A reference to another object in its most general form any mechanism that allows the holder of the reference to access the target object. The common implementation of a reference is to define a value that is a "pointer" to the referred object and an underlying mechanism that, given the "pointer" value, retrieves the object. In programming languages, the pointer may be a memory address, the look up logic in the memory heap and the associated class code to interpret the memory contents. In databases it may be a Table name, column name and value that represent a Foreign key/Primary Key pair, plus the database engine and its indexes to retrieve the appropriate record. In distributed systems a reference needs to identify the network address (the endpoint) where the object will be located plus an identification of the object local to the endpoint. Note that there may be other forms of "reference" for an object, for example an assertion on the properties of the object that uniquely identify it.

References between objects may have associated meaning or interpretations, providing the way to describe relationships between objects like "father of" or "supported by".

## Patterns

The Objects in a domain can be arranged in [patterns](https://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612/?&_encoding=UTF8&tag=saldubatechno-20&linkCode=ur2&linkId=205da23e03bd852215de12c4a7afac05&camp=1789&creative=9325) which are significant in the description of the domain. The usefulness of patterns is that they can describe the behavior of groups of objects independent of specific properties of those objects, similarly to how [abstract algebra](https://www.amazon.com/Book-Abstract-Algebra-Second-Mathematics/dp/0486474178?&_encoding=UTF8&tag=saldubatechno-20&linkCode=ur2&linkId=4cfde7ed3085580849f7f6a187286bf5&camp=1789&creative=9325) allows us to reason about the structure and behavior of sets without knowing all the specifics of the elements of those sets. Most programming languages and tools provide the basic patterns of collections (lists, lets, maps). Languages that provide [Generics or Templates](https://en.wikipedia.org/wiki/Generic_programming) in their type system directly support the definition of patterns by developers, with some languages (e.g. [Scala](https://www.scala-lang.org/)) providing higher level generics that support very sophisticated modeling of a domain's structure.
