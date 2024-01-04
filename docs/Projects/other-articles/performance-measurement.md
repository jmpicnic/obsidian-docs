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

- Effectiveness
  - Footnote on Efficacy (from health sciences)

- Efficiency

- Control

## Foundational Concepts

### A System Model

```plantuml
@startuml

!include style.ipuml

skinparam ranksep 20

left to right direction

control "Inputs\n(Jobs)" as Inputs
queue waiting
rectangle "\nSystem\nunder\nMeasurement" as System {
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
c2 --> Scrap
c2 --> Outputs
System <-l- Resources: consumes

(arrival\ntime) -> c1
(start\ntime) -> accept
(completion\ntime) -> done



@enduml
```

- Inputs (Jobs)
- Waiting
- System
  - accept
  - done
- Check: Simplification --> Instantaneous, does not require work or resources (i.e. included in system)
- Outputs
- Scrap
- Resources

### Counts vs Quantity

- Counts
- Quantities
- Value & Cost as quantities

### Periods

- Sampling Period
- Measurement Period
- Reporting Period

### Measurements vs Metrics

- Measurement: A count or a value directly extracted from the system at a point of time or for a period of time.
- Metric: An statistical calculation that combines measurements over time.
  - Averages/Means
  - Medians & Percentiles (e.g. P95)

## Basic Measurements

- Jobs/Inputs arriving per period of time
- Outputs produced per period of time
- Scrap per period of time
- Time of arrival of a job
- Time of acceptance of a job
- Time of completion of a job
- Jobs waiting
- Jobs in process
- Resources consumed per period of time
- Resources consumed for each specific job.

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

