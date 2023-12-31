---
author: Miguel Pinilla
Copyright: (c) Miguel Pinilla, All rights reserved
License: "This work is licensed under the Creative Commons License CC BY-NC-SA 4.0: https://creativecommons.org/licenses/by-nc-sa/4.0/"
email: miguel.pinilla@saldubatech.com
share: "true"
title: Overview
---

## The challenge of understanding supply chains

The definition of "Supply Chain" is fairly well understood as some variation of:

> Linked set of resources and processes between multiple tiers of developers that begins with the sourcing of products and services and extends through the design, development, manufacturing, processing, handling, and delivery of products and services to the acquirer. (From NIST: [supply chain - Glossary](https://csrc.nist.gov/glossary/term/supply_chain))

Taking this definition at heart implies that Supply Chain Management requires a widely broad set of disciplines and technologies that include fabrication and automation technologies, transportation and logistics, operations research, commercial contracts, import/export regulations, warehouse management, financing, etc...

It should not be a surprise that Supply Chain practitioners and Supply Chain Management (SCM) Vendors adopt narrower definitions or specialize in a particular aspect of it. A quick survey of the systems that touch activities associated with Supply Chains shows a true alphabet soup of acronyms like CMMS, WCS, WMS, SCM, TMS, etc. which reflects the very fragmented way supply chains are analyzed.

This fragmentation, while it has always been a problem, was overcome by dedicated professionals that would bridge the different aspects of a supply chain, or by ad-hoc integrations between information systems for particular companies and industries. Either solution was adequate when the timelines from orders or forecasts to delivered products were measured in weeks or even months and the value of a delivery was large enough to offset the costs of the required coordination. Two developments in the last ten years have upended this balance. E-commerce drives shrinking order-to-delivery lead times and a "long-tail" of product offerings, which makes it literally impossible to run traditional supply chain optimization systems based on a defined demand. Applying the "Lean Revolution" to supply chains requires a dramatic reduction of the levels of inventory that are considered acceptable, exposing supply chains to shortages and bottlenecks as they were experienced during the Covid pandemic.

In this new world, managing supply chains through a collection of systems that are integrated through legacy protocols (e.g. EDI standards dating back fifty years) is quickly becoming a losing proposition. In response to this, some industry groups and regulatory bodies are starting to propose more modern integration models like those proposed by the [*Digital Container Shipping Association*](https://dcsa.org/) (DCSA).

## Is it impossible?

The ambitious goal of creating a comprehensive, detailed description of supply chains may well be an impossible dream, at least for now. The difficulty of the problem should temper expectations of what standards can deliver. An overall, extensible framework of concepts and their associated structure should enable further progress and constructive collaboration. This approach is the one that the Open Systems Interconnect ([*OSI model - Wikipedia*](https://en.wikipedia.org/wiki/OSI_model)) seven layer model form ISO (the actual standard can be downloaded from [*ISO/IEC standard 7498-1:1994*](http://standards.iso.org/ittf/PubliclyAvailableStandards/s020269_ISO_IEC_7498-1_1994(E).zip)) took with great success in the telecommunications industry. This article proposes a similar model to understand and describe Supply Chains, which we intend to put to the test in follow up articles for the different layers and specialized aspects of those layers. It would be presumptuous to pretend that this first attempt gets everything or even most things right from the beginning. This article will be updated as we learn more and explore the different layers in later articles and hopefully enrich them with readers' comments and contributions.

## Five Layers of Supply Chain Operations

Similarly to telecommunication networks, supply chain networks and their behaviors can be approached from different viewpoints, furthermore, these viewpoints can be structured in a way that they build on each other to create a complete picture of Supply Chain operations.

The physical elements of a supply chain are the tangible parts that can be seen and touched like trucks, ships, warehouses, and other physical infrastructure. Together with other commercial and legal **Assets**, they are the foundation of the supply chain. The main operations in a supply chain are all about moving and storing wares and merchandise. Using assets as resources to perform these operations is the focus of a **Movements** layer that defines potential, planned and actual actions that Supply Chains perform. These actions are performed to make **Goods** available were they are needed. The goods layer will include the description of those goods and their end-to-end movement and transformation very much similar to how layer four of telecom networks (the transport layer) defines how data packages are sent end-to-end in a network regardless of the hops and routes they need to take, or in how many frames the transmission takes place. Goods are moved and transferred to service specific commercial **Transactions**. Transactions themselves will be represented by a number of documents (BOL's, Purchase Orders, etc..) and sub-transactions. Finally, Transactions take place between **Parties** in the supply chain and are performed within the rules set by **Contracts** and regulations.

The following table provides a summary of each layer. Following the lead of the OSI model, each layer defines a set of concepts in that layer, in addition, supply chains explicitly refer to networks of people and activities (see references below). Each layer is associated with business functions that are the most interested in the concepts and processes it defines.

|           | Domain                                                                     | Key Concepts                                                       | Users/Personas/Roles            |
|-----------|----------------------------------------------------------------------------|--------------------------------------------------------------------|---------------------------------|
| **Contracts & Business** | The overall business agreements, regulations, metrics and reporting that provide the framework for Transactions to be defined and executed. | - Service Level Agreements<br>- Credit Scores<br>- Compliance<br>- Risk<br>- P&L, Margin, Balances                                                                   | - Executive Management<br>- Financial Planning & Analysis                                                                              |
| **Transactions**         | The commercial transactions that inform and govern the movement, custody and ownership of goods within a Supply Chain.                      | - Orders<br>- Billing/Invoicing<br>- Service Costs<br>- Payments<br>- INCOTERMS<br>- Prices, Discounts, Promotions, …                                                | - Sales<br>- Purchasing<br>- Inventory Management<br>- Accounting (AR, AP, …)                                                          |
| **Goods & Shipments**    | The End-to-End view of supply chain operations from when goods are “shipped” in origin till when they are “received” at the destination     | - Cargo<br>- Inventory<br>- Ship<br>- Receive<br>- Logistics Service                                                                                                 | - Shippers<br>- Receivers<br>- Logistics and Warehouse Managers<br>- Brokers                                                           |
| **Movement**             | The Individual actions that are performed to discrete units of cargo.                                                                       | - Loads (things)<br>- Itineraries<br>- Transportation<br>- Storage<br>- Pack/Unpack<br>- Load/Unload (actions)<br>- Routing<br>- Transfers<br>- Value Added Services | - Operators<br>- Operations Planners<br>- Logistics & Automation Managers (Transportation, Warehouse, …)                               |
| **Assets**               | Provision, Manage and Operate the resources used in Supply Chain Operations                                                                 | - Facilities<br>- Vehicles<br>- Equipment<br>- Routes<br>- Catalog<br>- Parties                                                                                      | - Operators<br>- Owners/Lessees/…<br>- Facilities & Maintenance<br>- Long-Term capital & resource Planners<br>- Supply Chain Designers |

## Assets

The Asset layer is concerned with the Operation, Administration and Management of resources that are needed in Supply Chain Operations. These functions include (again, following the Telecommunications industry lead):

- Fault Management: Detect, Diagnose, Isolate and repair faults in assets.

- Configuration: Provision, Configure and maintain the information for an asset so that it is readily available for use and can be accounted for properly by its owners, operators, lessees, etc. It critically includes managing asset identifiers like container numbers, vessel IMO's, Vehicle identification numbers, license plates, etc...

- Accounting: Keep track of investment, costs, etc... associated with each asset and groups of assets.

- Performance: Define, monitor and report metrics for the performance of assets.

- Security: Manage and track the access and permissions for each asset, critical in establishing chain of custody auditability, fraud prevention and for certain sensitive operations in international or regulated trade.

Assets can be physical assets like a vehicle, a warehouse (facility) or a piece of automation equipment, legal assets like rights to routes or landing slots in airports, informational assets themselves like catalog information for SKU's or commercial assets like Vendors, Insurers, etc...

### Movements/Operations

The movements/operations layer focuses on the individual actions that are performed in supply chains. They treat the targets of those actions mostly as "opaque" items. A central example of such action is to move a sealed ocean container from one port to another or load/unload the container onto the ship. It may involve grouping/ungrouping cargo elements into other units (e.g. de-palletizing cases for retail) or it may also refer to legal or administrative actions like inspecting a container, clearing customs.

### Goods & Shipments

This layer's main purpose is to describe the movement of goods between two facilities, regardless of how those goods are packaged (e.g. they can be multiple truckloads or partial truckloads) or the specific operations that may be performed in the process. E.g. a Shipment is only concerned about the Shipping/Receiving activities, and not whether the movement is done through a single truck that travels directly, or through a series of LTL loads with intermediate cross-docking transfers. Although this example is taken from common trucking operations, the concept applies equally to automated transfer of goods within a warehouse or international trade. The unit of shipment may be different, but the focus on end-to-end movement of goods, and the identification of those goods is what is important.

### Transactions

Transactions are the commercial agreements that govern specific exchanges of goods and their associated shipments. These agreements are codified in well defined and regulated sets of documents with specific legal responsibilities. Orders (sales and purchase), when settled, represent the change of ownership of goods, BOL's and their lifecycle represent the change of custody of the affected goods, etc...

### Parties and Contracts

The final layer also represents commercial agreements between legal entities (Parties), but in this case these agreements describe the framework under which transactions are defined and executed. Contracts may define terms and conditions of payment between two parties that apply to all orders between them, etc... By extension, legal frameworks that govern transactions in a jurisdiction would also be included in this layer.

## Definitions of Supply Chains

A quick appendix with references to different definitions of Supply Chains

- Investopedia: [*The Supply Chain: From Raw Materials to Order Fulfillment*](https://www.investopedia.com/terms/s/supplychain.asp)

> A **supply chain** is a network of people and entities who are > involved in creating a product and delivering it to its consumer.

- NIST [*supply chain - Glossary \| CSRC*](https://csrc.nist.gov/glossary/term/supply_chain)

> Linked set of resources and processes between multiple tiers of > developers that begins with the sourcing of products and services and > extends through the design, development, manufacturing, processing, > handling, and delivery of products and services to the acquirer.

- McKinsey: [*What is supply chain and how does it function? \| McKinsey*](https://www.mckinsey.com/featured-insights/mckinsey-explainers/what-is-supply-chain)

> The supply chain is the interconnected journey that raw materials, > components, and goods take before their assembly and sale to > customers.

 - Council of Supply Chain Management Professionals (CSCMP): [*CSCMP Supply Chain Management Definitions and Glossary*](https://cscmp.org/CSCMP/Educate/SCM_Definitions_and_Glossary_of_Terms.aspx)

> \[\...\] all activities involved in sourcing and procurement, > conversion, and all logistics management activities

__________
Copyright: © Salduba Technologies, All rights reserved  
License: This work is licensed under the [Creative Commons License CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

