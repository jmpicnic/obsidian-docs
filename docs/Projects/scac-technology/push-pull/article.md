---
author: Miguel Pinilla
Copyright: (c) Miguel Pinilla, All rights reserved
License: "This work is licensed under the Creative Commons License CC BY-NC-SA 4.0: https://creativecommons.org/licenses/by-nc-sa/4.0/"
email: miguel.pinilla@saldubatech.com
share: true
title: Demystifying Push & Pull Operations
---

{{ draftMark }}

Pull systems in operations are nothing new. Toyota pioneered them in their renowned *Toyota Production System*[@onoToyotaProductionSystem1988] decades ago. A quick search in google for *pull systems*, *lean manufacturing*, *waveless operations* or similar prompts render a wealth of references. Technical books like Hopp & Spearman's excellent text[@hoppFactoryPhysics2011] provide in depth insights on the behavior of these systems, even the new AI Assistants like Google's Gemini know about the differences between Pull and Push systems when asked the right question:

> *\[\[Push operations produce based on forecasts, while pull waits for actual demand. Push keeps buffer stock,
> pull uses just-in-time inventory. Choose push for stable demand, pull for flexibility and lower costs.\]\]*

Despite all this information and knowledge, whole industries like warehousing or supply chain management are still trying to adopt them and even in manufacturing planning, the dominant ERP systems still cling to *Top-Down*, *Plan-and-assign* paradigms that characterize push systems.

## Boiling down the Push-Pull differences

Push and Pull policies aim to manage the performance of discrete item processing networks, a simplified view, but still very useful to reason about these systems includes:

1. Demand is received from an external source, typically in the form of orders to deliver a product or set of products by certain time. Orders arrive over time. In the technical lingo, *inter-arrival time* is the time elapsed between two consecutive orders arriving.
2. An *order release policy* selects the demand to be worked on and in which sequence.
3. Orders are processed by the system, consuming resources and taking up *processing time* until they are completed and delivered. To do this, the system must assign resources and capabilities (materials, labor, machine time, ...) to prepare the order.
4. Processing of an order may be successful, or may result in a failure to meet the product requirements. The ratio of successful completions over a period of time is called the *yield* of the operation.

![Simplified Operations View](assets/processing-system.drawio.png)

This very simple view is surprisingly powerful to gain insight into a broad range of operations. A coffee shop as an example, receives orders as customers walk in, processes them with a First-In-First-Out policy by the cashier and then the barista, and delivers the finished orders to the customer waiting to pick them up. Complex supply chains with multiple companies can also be analyzed in this way for an aggregate view of their operation.

For these systems, the traditional goal of operations planning is to:

> *Minimize the cost of the operation processing a given set of orders while complying with all the order conditions (including delivery times and quality)*

This formulation leads naturally to batching orders together to accommodate transportation constraints, minimize or eliminate set up times, tool changes, re-calibrations, etc., as well as stocking enough resources to complete at least one batch. This is the familiar solution adopted by how traditional MRP systems.

The first problem with this approach is hidden in the definition of the problem statement itself. It makes a number of assumptions that that end up creating a number of problems:

1. Demand is considered considered independent and unaffected by the characteristics of the operation. In reality, operations that deliver orders earlier will see their demand grow as the market realizes their advantage.
2. *A set of orders* is known to optimize against. In most real operations, demand will be composed of a number of *firm orders* mixed with a *demand forecast* that may have different levels of certainty depending on the industry, product mix, etc.
3. The condition and availability of resources is known and relatively stable from the time planning starts until the set of orders is complete. Provisioning for rush orders, disruptions, order cancellations, re-work etc. is done outside the planning process by using safety stocks, reserved capacity, etc. that degrade the performance of the *optimal* solution as a whole.
4. The processing capacities and processing times of the operation are also well known and stable over time. Note that this is a particularly tricky assumption, as processing capacity of any process is really difficult to assess in real-live conditions, yet it is an essential input to MRP systems.
5. The *yield* or quality of the operation is independent of the size of the batch or how much work in progress there is at any point in time.
6. Ramp-up and Wind-down of activities for a batch are short and do not represent a significant portion of the time resources are dedicated to a batch of orders, or alternatively two batches can overlap during these periods without significant impact to the operation.

The bogey man hiding behind these assumptions is ignoring the effects of variability on the performance of the system, or as Hopp & Spearman call it out, *The Corrupting Influence of Variability*[@hoppFactoryPhysics2011]. 

After looking at a lot of different operations, mostly in logistics and distribution, but also in manufacturing, my own take on the differences between these two approaches to plan and control operations boil down to:

