---
author: Miguel Pinilla
Copyright: (c) Miguel Pinilla, All rights reserved
License: "This work is licensed under the Creative Commons License CC BY-NC-SA 4.0: https://creativecommons.org/licenses/by-nc-sa/4.0/"
email: miguel.pinilla@saldubatech.com
share: "true"
---
Enterprise Resource Planning (ERP) systems originated in the manufacturing industry, and were initially used to manage production processes and inventory. They have since evolved to encompass a wider range of business operations, including financial transactions, supply chain management, human resources, and customer relationship management.

At a high level, the widespread success and ubiquity of enterprise resource planning systems in companies of all sizes and industries stems from their strengths in:

* Creating a reliable, auditable, and secure single source of truth for an enterprise, representing the state of its resources (financial, inventory, etc.) and a record of the business operations that the enterprise conducts.

* Supporting the definition, application, and compliance of standard processes and policies in the enterprise.

* Planning and optimizing the assignment of resources and the sequence of tasks for complex operations (e.g., manufacturing plans, order fulfillment, etc.) that are then executed through the standard workflows and processes.

The strengths of ERP systems have led vendors to expand the systems’ scope beyond their original focus on manufacturing and financial transactions. Today, ERP systems integrate many functions of a company, including Human Resources, Customer Relationships, Order Management, Purchasing, and more into a single system. For example, this [SAP tutorial](https://www.tutorialspoint.com/sap/sap_modules.htm) shows the broad footprint of one of the leading ERP providers.

The software architecture for ERP systems, although it has evolved over time, is essentially a three-tier system. It includes a unified data store (usually a relational database) to represent and persist the system’s state and history, a business layer that can be deployed as a monolith or as a collection of services, and a user interface layer based on web technologies. Additional integrations are also available to communicate with other systems, either within the same enterprise or across different companies (e.g. through EDI, SOAP, or other interface technologies).

Enterprise software architecture has been so successful that it has been codified into multiple development frameworks, the most famous of them in Java ( [JEE](https://www.oracle.com/java/technologies/java-ee-glance.html)), but available in most modern programming languages, and an industry of books, consultants and practitioners has grown around it.

As with many other technologies, the availability and maturity of these frameworks has led to their application to problems that do not quite fit the initial architectural pattern, but still benefit from the individual capabilities the frameworks offer, and in some cases, simply because it is a well understood architecture by the available engineering talent. JEE or its close relative [Spring](https://spring.io/), for example, has been applied to a wide range of problems, from warehouse automation to equipment maintenance, web and content portals, and more. In particular, multiple supply chain management systems have been built using this architectural pattern.

# ERP’s are built to plan the resources of enterprises

The headline is a stupid-sounding, self-evident statement but it is frequently forgotten when trying to apply the same technologies, patterns and systems to supply chains. Supply Chains are not Enterprises, cannot be described simply in terms of resources and cannot be planned, if we accept this bold statement, it should not be a surprise that ERP systems are ill fitted to support supply chain management activities. We need to unpack this statement to understand why ERP systems are not applicable to Supply Chain Management and identify what an SCM system architecture should look like.

## Supply Chains are not Enterprises

This should be an obvious statement, as a Supply Chain, more properly a Supply Networks includes multiple independent companies including vendors, clients, logistics providers, etc…

Any system that aspires to support Supply Networks needs to take into account:

 1. Independent companies have private information that they do not wish to share with other companies, including data sources and facts that directly impacts the picture they have of the state of the world. As an example, a consignee of a shipment may have paid for premium tracking equipment and services for the pallets that carry their goods, gaining precise positioning not only of their pallets, but also of the trucks that carry them in LTL shipments. They may not be willing to give this information to others because it allows them to better forecast their inventory positions and if the position of the truck is known to other consignees in the same truck, they would derive the same benefit without having to pay for the premium tracking service. This example shows that different participants in a supply network may event have different views of the “reality” of the state of assets in the real world which the SCM system needs to reconcile.

 2. Companies that do business with each other want to share certain information regarding their transactions with a single ***source-of-truth***, while keeping their private information for those same transactions to themselves. It is common that a single transaction (e.g. a shipment) has more than two parties to it (e.g. Shipper, Consignee, Carrier, Buyer, Vendor, Insurer, Broker, …) and the access that each party has to the transaction data and actions is determined by the business relationship of the party to that transaction. SCM systems need to support a very fine grained permission and access control system that follows those business relationships between parties and transactions.

 3. Companies have their own internal information systems to manage their operations. These systems are not compatible with each other, not just in the technologies they use, but in the assumptions they make, the concepts they implement and the policies they enforce. An SCM system must provide a shared information model and clear technical and business protocol specifications for companies to join a supply network. This is not a new concept in the analog world of commerce, where the protocols between companies are embodied in price and availability signals, commercial documents like invoices, payments, bills of lading, purchase orders, etc… and the complex “Terms and Conditions” associated with contracts and transactions.

## Supply Chains are more than Resources

The concept of resource in the ERP world stems from the original Manufacturing Resource Planning systems where a resource is a representation of an asset or a capability used to carry out business operations. ERP/MRP Systems make three critical assumptions regarding resources:

The concept of resource in the ERP world stems from the original Manufacturing Resource Planning systems where a resource is a representation of an asset or a capability used to carry out business operations. ERP/MRP Systems make three critical assumptions regarding resources:

 1. The system has complete visibility and access to the attributes and state of the resource. E.g. the system ***knows*** what the levels of inventory by SKU are for each raw material.

 2. The system is the only one that assigns and consumes resources to perform business operations. All usage of resources goes through the system.

 3. Information on the state and availability of a resource is accurate and up-to-date in the system. The system provides very limited capabilities to consider uncertain or noisy information regarding resources when planning or executing business operations.

In supply chain operations, none of these assumptions are true:

 1. Information about resources is sometimes private to a party which does not wish to share it. E.g. A supplier may not want to share the inventory levels it carries internally as described in the previous section. Even when the information is willingly shared between trading partners, integration technologies and mis-matched data models between systems frequently prevent full sharing of information.

 2. In a supply network, resources, in the sense of ERP/MRP are subject to changing demands and availability from multiple sources. Even in the case where certain availability is “guaranteed” by a vendor, that does not mean a 100% assurance that it will not change, either due to unavoidable real world incidents (trucks break down, inventory is lost) but also because of possible vendor policies like airline overbooking. Some of these issues are also present in the confine of an ERP/MRP system (e.g. damaged goods in a warehouse effectively reduces the availability of inventory), but the broader scope of supply chains makes this problem much more prevalent and needs to be addressed directly.

 3. Updates to the state of resources are not transactional and may be received out of order with respect to when they happen. Even when the information is available, either because it is public information or it is shared through a data feed, it originates on disparate systems, connected to different communication protocols, which may include batch processing, EDI, etc… Furthermore, different data sources may provide contradictory or inconsistent information about the same resource. E.g. EDI feeds from a shipping company may provide arrival times that are not consistent with what GPS/AIS signals estimate.

## Supply Chains cannot be planned

ERP/MRP systems implement detailed workflows and processes to support business operations. Implicit in this view is the fact that the organization will follow those workflows when carrying out the plans the system generates and will report results and incidences to the system so that it can adapt and correct the plans if necessary.

As mentioned in previous sections, supply networks are composed of independent companies with their private information, and the state of resources is at best uncertain and noisy. These would be reason enough to justify the statement that supply chains cannot be planned in the traditional sense of ERP/MRP systems. In addition the different parties in a Supply Chain have their own goals, priorities and agency that cannot be formulated through an “objective function”, no matter how complicated or “AI enabled” we make it. Even if we somehow managed to create a plan for a supply network, the level of uncertainty and disruption from the environment and from parties is too high, rendering any potential plan obsolete the moment it is completed and published.

Supply Chains nevertheless work effectively every day without the need for a central planner to intervene. They naturally rely on [market based optimization](https://user.it.uu.se/~arnea/ps/markOpt.pdf) even if they don’t apply those algorithms explicitly. Supply chains exchange market signals (price, availability, lead times, etc…) and parties use those to determine what actions to take instead of using detailed resource information as traditional planning systems do.

# Where do we go from here

So, if the most prevalent architectural approach to business systems is not adequate to handle supply chains, what is the alternative? It would be incredibly arrogant to try to propose a complete framework to build supply chain systems at this point, as there is still a lot of unknowns and uncertainty regarding technologies and also the specific requirements for these systems, yet some elements are emerging that are worth pointing out and that will be topics for other articles:

* SCM system must be able to represent the “real world” with its complexity stemming from updates that may come out of order, access to different data streams, variable latency and asynchronous communication. [CQRS architectures](https://martinfowler.com/bliki/CQRS.html), modeling streams of update requests explicitly are a strong candidate to model these systems

* Persisting the journalled state of the system is also needed to provide an auditable source of information for decisions and actions. [Bitemporal Databases](https://en.wikipedia.org/wiki/Bitemporal_modeling), with their ability to represent the state of the world at a point in time (effective time) as known at a different point in time (recorded time) go a long way to support this requirement of data data representation. Augmenting these with a concept of “workspace” defined by the data streams that are accessible from it have the potential to support the need to represent multiple private versions of the same information.

* Authorization and access decisions based on [ABAC](https://en.wikipedia.org/wiki/Attribute-based_access_control) type of policies are needed to implement the fine grain access control to information required by multi-party interactions. The attributes that support the access decisions need to be driven by the “agency” capabilities of the different parties in relation to the transaction or data record with an ***Agent-For*** based permissioning structure.

* Communication between systems must mimic real world inter-company communications which are asynchronous much more often than synchronous. Subscription Webhooks or streaming communications must become as well supported as RPC style protocols are today (e.g. [REST-OAS3,](https://swagger.io/specification/) [SOAP](https://www.w3.org/TR/soap/) or [gRpc](https://grpc.io/)).

* The information that these protocols will interchange will need to follow the model of market signals, exceptions, etc… To represent commitments between SC parties, communication protocols need to support non-repudiability (qualified with validity intervals, etc…) will need to be ensured along with the standard privacy and security mechanisms.

* Data acquisition for these systems will need to make decisions on the veracity and certainty of the information that data sources provide, including assessing multiple, possibly inconsistent data sources. Data Science techniques of likehood maximization and estimation, including Machine Learning models will need to be brought to bear as smart ingestion engines that generate the update requests for the core CQRS based data authorities mentioned above.

* Interpretation of the “best guess” of the system state contained in a workspace also needs to be customized for the different consumers of the information as their use and internal policies will vary among the parties in a supply chain. Explicit “interpreter” modules that post-process the information and changes to it will be needed to feed operations workflows and actions.

Although these points do not constitute a full blueprint for SCM systems, they point to architectures and technologies that are much more reactive and real-time based than traditional ERP systems and suggest areas of exploration for technologists faced with the challenge of building these systems. Stay tuned for future posts on some of these topics as they become a bit clearer in our minds.
