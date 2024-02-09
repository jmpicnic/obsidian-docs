---
author: Miguel Pinilla
Copyright: (c) Miguel Pinilla, All rights reserved
License: "This work is licensed under the Creative Commons License CC BY-NC-SA 4.0: https://creativecommons.org/licenses/by-nc-sa/4.0/"
email: miguel.pinilla@saldubatech.com
share: true
title: The Drunk, their keys and a lamp post
---

The story goes like this. A drunk is searching for something at night around a lamp post. A passerby, seeing the distress, starts a conversation trying to help.

![Image from https://sketchplanations.com/looking-under-the-lamppost](assets/looking_under_lamppost.png){width="40%", align=left}
&larr; *What are you looking for? Can I help?*
&rarr; *I am looking for my keys but I can't find them.*
&larr; *I'll help you look for them, where did you lose them?*
&rarr; *I lost them over there in that bush.*
&larr; *Hmm, why are you looking for them here then?*
&rarr; *There is no light over there, I won't see them, Duh!*


<br><br>

What makes this joke funny is not that we laugh at a hapless drunk, but rather that we see ourselves somewhat reflected in the drunk's predicament.

With measurement, and in particular with performance measurement, we are like the drunk in the story, looking for *easy* indicators and metrics instead of looking for those that will actually lead to good decisions and results. How can we otherwise explain the prevalence of trying to measure productivity by lines of code or number of pull requests, employee's performance by number of hours in the office, health of an economy through their stock market and endless of other cases of misuse of indicators. The only difference with the story is that both the metrics involved and the result we seek are more sophisticated or complex than simple keys and light.

In business or engineering the drive to measure performance for a system or organization is to inform decisions on how to operate it, or what changes need to be made to get the maximum possible value in exchange for consumed resources. The need to support decision making should make us very wary of lamppost situations and not be happy with whatever data is readily available without making sure that it does represent the outcomes that we want to control.

The seemingly foolproof formulation of *maximum value in exchange for consumed resources* kicks the can down the road by not defining what *value* and *resources* are, and what observations will accurately represent the value produced and the resources consumed.

Definition of value and resources is very dependent on the field of application. Some industries, like chemical production, can define it very clearly based on the volume or weight of products and reactants, while in others, like design or engineering activities, both the value and the resources are much harder to define and measure. They are sometimes measured by *story points*, design artifacts, hours of engineering, etc... There are reams of literature in different fields addressing this problem. In this article we are after the more modest goal to outline a systematic way to approach the measurement problem itself, with a general formulation of value and resources that can be mapped and refined in specific fields.

## Back to Basics

In keeping with the spirit of the *Impractical Engineer*, the definition of *Performance* by [Merriam-Webster, fourth meaning](https://www.merriam-webster.com/dictionary/performance) refers itself to [Perform](https://www.merriam-webster.com/dictionary/perform), which gives us the baseline for the context of performance measurement:

1. Carry out something, typically a task or jobs.
2. Adhering to terms (as in a contract) and expected results

So we can adopt for our purposes:

> Performance is the execution of tasks or jobs subject to certain terms and expected results

This broadly accepted definition of performance still leaves out how to map performance to real world value, hiding behind the generic terms of completion of *tasks*, *terms* and *expected results*.

Despite these limitations, these concepts, and the framework that derives from them are powerful tools to structure and implement performance measurement mechanisms, as they can be more easily mapped to different fields.

### Effectiveness and Efficiency

There are two aspects of Performance commonly considered.

Effectiveness
: How well is are jobs performed against the given terms. That is how much or little the results of the job deviate from the expectations/terms.

Efficiency
: How many and what kind of resources are used in completing the jobs. Similarly, there may be expectations (terms) on the quantity and type of resources used that are considered when evaluating performance.

The immediate goal of Performance Measurement is to define and obtain metrics that allow to observe and evaluate the performance of a system (people, machines or combinations of both) when executing a task. Evaluation of performance in turn has an ultimate goal to understand the behavior of the system and be able to control and improve it by effecting changes in it.

## A Framework for Performance Measurement

To bridge the gap from the previous definitions to an actionable formulation of performance metrics we need to:

1. Adopt a model of the system that we intend to measure so that we can define how to observe it and make the definition of jobs, resources and results concrete and measurable.
2. Have a clear picture of the measurement process, that is, how to go from observations of the system to a set of metrics and indicators that faithfully represent the performance behavior of the system.
3. Define what specific observations and calculations on them will be implemented in the measurement process.

### System Model and Performance Indicators

The `System` to be measured and controlled performs `Jobs` that are presented to it as `Inputs` through a `waiting queue` and deliver the results of its activity as `outputs` if they meet the expected terms, or rejected as `scrap` if they don't meet the expected terms. The `System` consumes `Resources` to perform the jobs in its input queue.

The delivery of value is a function of the jobs successfully completed. The simplest interpretation is to assign a constant, uniform value to all jobs completed with more sophisticated models will evaluate it based on domain dependent characteristics of the completed jobs. In Agile software engineering this would be equivalent to assigning value based on the raw number of *stories* completed vs. the sum of their *story points*.

Value is then associated to how many jobs are completed in a unit of time, and how quickly a job is completed from start to finish.

A very simplified system model can be represented graphically as a *job flow* diagram:

```plantuml
!include ../../Projects/other-articles/performance-measurement/system-model.puml!OBSERVABLE_SYSTEM
```

Where *jobs* are generated in an external *Input* process and arrive to the system through an *entry* point. Jobs wait in a queue until the system *accepts* them to work on them. The System consumes *Resources* working on jobs and delivers jobs when each of them is *done*. Jobs that are *done* can be successful (matching the terms and expected results) or not. This is determined by a *check* that, for the purposes of this model is instantaneous and does not consume resources. Note that any time or resources consumed by the check can be bundled in the general processing of a job within the system. The *check* determines whether each job is successful (an *output* of the system) or not (the system producing *scrap* that can be considered of no value for the purposes of this simplified model).

Based on this model, both Effectiveness and Efficiency can be further refined into performance indicators like:

- `Yield` is the first indicator of *adherence to terms* for the execution of a job. While the specific terms vary greatly from application to application, the system abstraction allows us to study the relative frequency of successful outputs vs unsuccessful scrap.
- `Throughput` is the rate at which the system generates *successful* outputs. Higher throughput drives higher value generation.
- `Wait Time` is the time elapsed between the arrival of a Job and when the system starts processing it. It shows the *idle* time that jobs must endure, and therefore potential loss of value or opportunity.
- `Processing Time` is the time a job spends between their start event and their completion event.
- `Lead Time` is the total time between the arrival of a Job and its completion event. It is important to qualify whether this is for all jobs or only successful ones. Lead time is the combination of `Wait time` and `Processing Time`. Its value as an indicator is to highlight the delay between the time when a commitment to spend resources is made (job arrival) and when the value associated with that job is realized.
- `WIP` (Work in Progress): An assessment of how many jobs are simultaneously being performed by the system. It can be a simple count of *active* jobs or calculations based on other values associated with a Job like the money value of a job, the number of individual items in the job (e.g. how many items in a shopping order), etc. As an indicator, it is a direct measure of how much value is *trapped* in the system at a particular point in time.
- `Resource Usage per unit of Yield`: Usage of a specific kind of resource used either in the period or for a job. For simplicity, in the diagram above, there is no detail on the lifecycle of resources, but typically they have a *Consumption Event* with an associated time when a quantity of the resource is consumed (if it is discrete) or a *Consumption Rate* for continuous consumption (e.g. electricity)

As mentioned before, this is a very simplified model of system operation, but it provides enough elements to define the fundamentals of observation and measurement and captures the essence of operations for a very broad range of business and technical processes, a very short list of very common applications of this model include:

Call Centers
: The jobs here are incoming calls, the execution of the job is to respond to customers questions or requests, If the customer is satisfied, it is a successful outcome otherwise it is considered scrap.

Telecommunication Systems
: Jobs are either connection requests or data packets to be routed.

Supermarket Cashiers, Coffee shops, etc...
: Jobs are customer checkouts or services to render (serving coffee)

API Calls for information systems
: Jobs are API requests that can succeed or fail and take a time to produce a response (output) or an error (scrap)

Software or Engineering Design Teams
: Jobs are defined as "units of work" like Stories in agile methodologies or WBS tasks in more traditional project management.

Accounts Payable/Receivable
: Jobs are invoices that arrive when the accrual happens, they start when the invoice is issued and are complete when the invoice is settled or considered delinquent.

Manufacturing Processes
: This application (together with the telecommunication systems) is where the model originated, with jobs being actual jobs to create a product.

## The Measurement Process

The definition of Indicators is a strong starting point, but they are not yet actionable to implement a performance measurement program. To do this, we need to define measurements and metrics, and the process to obtain them. To really understand what we are doing when implementing a performance measurement system, we need to lay the foundation of measurements, metrics, etc...

A [measurement](https://en.wikipedia.org/wiki/Measurement) is the *quantification of attributes of an object or event*. Measurements are obtain through by assigning numbers or other symbols to observed phenomena following a consistent set of rules.

In the context of performance measurement, we will use a narrower definition for measurement and complement it with other concepts to better structure the measurement process:

Signal
: An observable phenomenon which can be continuous (e.g. the voltage of a battery) or discrete (e.g. arrivals of jobs to a system for processing).

Measurement
: The act of assigning a number, typically with an associated unit to a Signal associated with a particular moment in time.

Metric
: A Calculation based on one or multiple measurements that generates a value (a number or other symbol) that provides quantitative information about an Indicator.

Metric Presentation & Evolution
: The presentation of how a metric changes over time to the end users that need to exercise judgments and actions based on the values of the indicator metrics.

Signals, Measurements and Metrics take place within the passage of time and, although theoretically some could be considered *instantaneous* or *continuous*,in any practical implementation, they all take a duration, or can happen only at particular moments in time. The calculations and presentation of measurements and metrics need to take this into account and convey the information about the time when signals are observed, what periods of observation are used for calculations and the overall period that a particular report or graph represent.

## Performance Measurements and Metrics

Applying the concepts in the measurement process to the performance indicators, we can finally define the actionable measurements and metrics to characterize the performance of a system.

The measurements that we can take from a system represented by the model above are:

- *Yield*
  - Number of jobs successfully completed in the period
  - Number unsuccessful jobs in the period

- *Throughput*
  - The same measuremetns as for *Yield*
  - Number of Jobs arriving to the system in the period
  - Number of Jobs started processing in the system)

- *WIP*
  - The number of jobs present in the system at the beginning or end of the sampling period. It is important to pick one of the two points and be consistent about using it to take measurements.
  - The number of jobs concurrently being processed by the system (jobs that have started by not completed)
  - The number of jobs waiting to start processing

- *Wait Time, Lead Time, Processing Time*
  - Time of each job to start processing since it arrives
  - Time of each job to complete since it starts processing
  - Time of each job to complete since its arrival

- *Resources Consumed*
  - Resources (by type, or aggregated through a common attribute like cost) consumed during the sampling period
  - Resources consumed in the processing of a specific job.

Note that in these definitions we are *simply counting* jobs and not trying to measure the value associated with each job or accumulating the multiple jobs into a "value measurement". The underlying assumption is that the variability of value between jobs is relatively small. If this is not the case, the most common approach is to divide the population of jobs into multiple *job classes*, each of them relatively homogeneous w.r.t. value and behaviors. Alternatively, a job may be attributed with additional characteristics which can then be used to compute value metrics.

Metrics are the key artifact to support decision making. It is not possible to prescribe a single, uniform set of metrics for performance measurement that is applicable in all situations and use cases. As an alternative, we can aim to define some stereotypical metrics that can be specialized or refined for specific applications.

Yield
: Yield metrics are computed based on the Yield measurements for the period, the percentage of failures with respect to all completed jobs, $yield = N(unsuccessful) / N(successful)$

Throughput
: Throughput metrics tend to follow closely the measurements defined above. Throughput metrics introduce and additional consideration of "reference" levels chosen based on the intended use of the metric:

- Target goals (e.g. desired visitors to a commerce web site) to measure business performance against expectations.
- A statistic computed over longer periods, typically the historical average or a high percentile (e.g. p80, p90) to detect trends or changes in the behavior of the system or job arrival.
- An estimate of Capacity (See below as resources) of the system to serve as an alert signal that a resource or an internal process in the system may become bottlenecks and create problems.

Wait Time, Lead Time, Processing Time
: These measurements are job specific and metrics are needed to get an aggregate view of the system behavior. The most common metrics are centrality statistics like median, average or mode across all considered jobs. Service Level Objective metrics (SLO's) are computed as dispersion statistics like standard deviation or *limit* statistics like P90 or P95 of the population of jobs.

Resources Consumed
: Although the specifics of resource consumption depend a lot on the particular application, all applications share the fact that the maximum throughput of the system is limited by the capacity of its *bottleneck*. Based on this Capacity, we can define the metric of *Utilization* with is simply the Throughput expressed as a fraction of the maximum throughput.

## Follow up

We have tried to provide an introduction and summary of the core concepts to build a performance measurement system, we will be providing more details in other articles about:

* Mechanics and math of Measurements and Metrics
* An extended system model and how to use it to pick metrics to support decisions
* An example of application to API Endpoint Observability

Stay tuned.