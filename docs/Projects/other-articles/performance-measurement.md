---
author: Miguel Pinilla
Copyright: (c) Miguel Pinilla, All rights reserved
License: "This work is licensed under the Creative Commons License CC BY-NC-SA 4.0: https://creativecommons.org/licenses/by-nc-sa/4.0/"
email: miguel.pinilla@saldubatech.com
share: true
title: The Impractical Engineer: Performance Measurement
---

{{ draftMark }}

## The goals of performance measurement

As usual in the *Impractical Engineer* series, we want to ground ourselves on the foundational concepts. The definition of *Performance* by [Merriam-Webster, fourth meaning](https://www.merriam-webster.com/dictionary/performance) refers itself to [Perform](https://www.merriam-webster.com/dictionary/perform), which gives us the baseline for the context of performance measurement:

1. Carrying out something, typically a task or jobs.
2. Adhere to terms (as in a contract)

So we can adopt for our purposes:

> Performance is the execution of tasks or jobs subject to certain terms

There are traditionally two aspects of Performance

Effectiveness
: How well is the job performed with respect to the given terms. That is how much or little the results of the job deviate from the expectations.

Efficiency
: How many and what kind of resources are used in completing the jobs. Similarly, there may be expectations on the quantity and type of resources used that are considered when evaluating performance.

The immediate goal of Performance Measurement is to define and obtain metrics that allow to observe and evaluate the performance of a system (people, machines or combinations of both) when executing a task. Evaluation of performance in turn has an ultimate goal to understand the behavior of the system and be able to control and improve it by effecting changes in it.

To understand performance measurement in depth, it is useful to adopt a model that shows how these concepts work together.

## A Systems Model

The diagram below shows a `System` that performs `Jobs` that are presented to it as `Inputs` through a `waiting queue` and deliver the results of its activity as `outputs` if they meet the expected terms, or rejected as `scrap` if they don't meet the expected terms. The `System` consumes `Resources` to perform the jobs in its input queue.

```plantuml
@startuml

!include style.ipuml

skinparam ranksep 20

left to right direction

control "Inputs\n(Jobs)" as Inputs
queue waiting
rectangle "\nSystem\nunder\nObservation" as System {
  portin accept
  portout done
}
rectangle Outputs
rectangle Resources
rectangle Scrap

circle . as c1
hexagon check as c2

Inputs --> c1
c1 --> waiting
waiting --> accept
done --> c2
c2 --> Scrap: unsuccessful
c2 --> Outputs: successful
System <-l- Resources: consumes

(arrival\ntime) -> c1
(start\ntime) -> accept
(completion\ntime) -> done

@enduml
```

There are three key events in the processing of a `Job`, with their respective times when they happen:

- Jobs arrive to the system at the `arrival time`
- The System starts processing a Job (accepts it) at the `start time`
- The System completes processing a Job at the `completion time`

## Applications of the model

This simple model can capture the essence of operations for a very broad range of business and technical processes, a very short list of very common applications of this model include:

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

## Performance Indicators

Using the concepts in the previous section, we can add rigor to the definition of performance given at the beginning by defining key indicators or values that we can observe in the model. These indicators provide guidance on what measurements and metrics need to be defined to rigorously assess the performance of the system.

### Effectiveness Indicators

- `Yield` is the first indicator of *adherence to terms* for the execution of a job. While the specific terms vary greatly from application to application, the system abstraction allows us to study the relative frequency of successful outputs vs unsuccessful scrap.
- `Throughput` is the rate at which the system generates *successful* outputs
- `Wait Time` is the time elapsed between the arrival of a Job and when the system starts processing it.
- `Lead Time` is the total time between the arrival of a Job and its completion event. It is important to qualify whether this is for all jobs or only successful ones.
- `Processing Time` is the time a job spends between their start event and their completion event.
- `WIP` (Work in Progress): An assessment of how many jobs are simultaneously being performed by the system. It can be a simple count of *active* jobs or calculations based on other values associated with a Job like the money value of a job, the number of individual items in the job (e.g. how many items in a shopping order), etc.

### Efficiency Indicators

- `Resource Usage per unit of Yield`: Usage of a specific kind of resource used either in the period or for a job. For simplicity, in the diagram above, there is no detail on the lifecycle of resources, but typically they have a *Consumption Event* with an associated time when a quantity of the resource is consumed (if it is discrete) or a *Consumption Rate* for continuous consumption (e.g. electricity)

## The Measurement Process

The definition of Indicators is a strong starting point, but they are not yet useful for actually getting measurements and metrics of the system under observation. Obtaining values for those indicator require applying a measurement process.

A measurement process is a mechanism to assign numbers or other symbols to observed phenomena following a consistent set of rules. In keeping up with the rigor we aspire to, we will use the definitions:

Signal
: An observable phenomenon which can be continuous (e.g. the voltage of a battery) or discrete (e.g. arrivals of jobs to a system for processing). Clearly, signals are constrained by the observation technology available and the nature of the observed phenomenon. This obvious statement is important when designing observability tools and to understand the limitations of the observations. E.g. if a voltmeter is only able to take measurements every second, we'll never be able to properly measure oscillations in the Megahertz range and Measurements and Metrics built on these signals need to know these limitations to avoid mis-representing their results (e.g. a sinusoidal Mhz signal would show basically as zero in this example). More practical examples are that we won't be able to detect traffic surges to a website if we only count requests once an hour and similar situations.

Measurement
: The act of assigning a number, typically with an associated unit to a Signal associated with a particular moment in time. E.g. Using a voltmeter to read the number of *Volts* in the voltage signal above or counting the number of jobs in the waiting queue in the system. Assigning a single measurement to a signal is necessarily susceptible to inaccuracies and noise from the source of the signal itself, the measurement instrument, environment, etc. and it is important to consider the nature of this noise when designing the metrics that will use the measurement in order to minimize the effect of the expected noise.

Metric
: A Calculation based on one or multiple measurements that provides a value (a number or other symbol) that provides information about an Indicator. These calculations can be from an assignment of a color to certain values (Green-Yellow-Red) to sophisticated descriptive statistics of multiple measurements like means, percentiles, standard deviations, etc.

Metric Presentation & Evolution
: The presentation of how a metric changes over time to the end users that need to exercise judgments and actions based on the values of the indicator metrics.

Signals, Measurements and Metrics take place within the passage of time and, although theoretically some could be considered *instantaneous* or *continuous*,in any practical implementation, they all take a duration, or can happen only at particular moments in time. From the discussion above we need to identify the following time periods:

Measurement or Sampling Period
: The time between two consecutive measurements of the same signal. This needs to be short enough to capture the details we want from the underlying signal. A period of half the time of the smallest expected changes is a widely accepted value based on [Nyquist Theorem](https://en.wikipedia.org/wiki/Nyquist_frequency)

Calculation Period
: The time (or alternative the number of consecutive measurements) that will be considered in the calculation of a metric value. The length of the calculation period is obviously bounded by the Measurement Period itself on the lower side and by the loss of resolution on the upper side. It needs to be long enough to reduce the expected noise in the measurements to an acceptable level. The distribution of the [Sample Mean](https://en.wikipedia.org/wiki/Sample_mean_and_covariance) is a good guide to decide how big this period should be.

Metric Interval
: The period between the calculation of two consecutive metrics. Although in many cases this is the same as the Calculation Period, some Metrics require different Metric Intervals. A well known example is the Monetary Annual Inflation that is reported every month (Metric Interval) but computed over the trailing 12 months (Calculation Period)

Reporting Period
: The length of time for which multiple metric values are displayed together for evaluation. This is the *length* of the $x$ axis in most graphs that show metrics over time.

With these concepts in hand, it is pretty much trivial to define the Measurement Process in simple steps:

1. The signal is observed during the sampling period and a value is obtained by an instrument or probe as a measurement associated with that time period.
2. A set of measurements (in general from one or multiple signals) are collected during the calculation period and, at its end, a calculation is performed to obtain the value of the metrics associated with that period.
3. Step #2 is repeated every Metric Interval
4. At the end of the Reporting Interval or later, all metrics for that period are collected and displayed together for analysis typically in the form of a table or graph.

## Measuring the Performance Indicators

Although the concepts of signals, measurements and metrics are applicable to continuous and discrete phenomena, for the type of system described above, the main interest is their application to discrete phenomena and signals.

### Measurements

For discrete processes, there are two types of measurements possible:

1. Snapshot measurements: Measuring the current count of jobs present in the system during the sampling period
2. Flow measurements: Measuring how many jobs arrive, start or complete during the sampling period.

Either measurement may be based on simple counts of jobs, or use another derived measurement that takes into account specific difference between jobs. E.g. in an Accounts Payable process it is customary to use the value of the payable invoices and the measurement of choice instead of the number of invoices themselves, while in a call center, it is much more likely to measure the number of calls answered or in process rather than other characteristics of the call. The choice of the measurement is driven by:

- The impact on performance of the variation between jobs (e.g. the value of invoices may vary a lot and has key impact on the performance assessment of the process)
- How difficult it is to observe other derived characteristics of the jobs
- How reliable are the observations of these derived characteristics.

<!-- Yield, Throughput, Wait time, Lead Time, Processing Time, WIP -->

For the system shown above, the measurements are restricted to counting jobs or simple derivations of job characteristics (e.g. the sum) during the sampling period. The possible measurements are:

- *Yield*
  - Number of jobs successfully completed in the period
  - Number unsuccessful jobs in the period
- *Throughput*
  - The same values as for *Yield*
  - Number of Jobs arriving to the system in the period
  - Number of Jobs started processing in the system)
- *WIP*
  - The number of jobs present in the system at the beginning or end of the sampling period. It is important to pick one of the two points and be consistent about using it to take measurements.
  - The number of jobs concurrently being processed by the system (jobs that have started by not completed)
  - The number of jobs waiting to start processing
- *Wait Time, Lead Time, Processing Time*
  - Time of each job arriving to the system
  - Time of each job starting processing
  - Time of each job to complete.
- *Resources Consumed*
  - Resources (by type, or aggregated through a common attribute like cost) consumed during the sampling period
  - Resources consumed in the processing of a specific job.

## Metrics

### Effectiveness

- Yield
- Throughput
- MTBF
- Lead Time
  - Arrival to Done
  - Acceptance to Done
- WIP
  - Waiting
  - Active
- Resource Usage

### Efficiency

- Resources per unit of output
- Resource WIP

## Developing Intuition

- M/M/1
- 

## Applications

### API Performance

### Streaming/Messaging System

### Software Development

### Manufacturing

### General Operations (Cust. Support, Cashiers, ...)

