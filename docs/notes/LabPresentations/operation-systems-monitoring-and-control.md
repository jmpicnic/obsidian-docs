---
author: Miguel Pinilla
Copyright: (c) Miguel Pinilla, All rights reserved
License: "This work is licensed under the Creative Commons License CC BY-NC-SA 4.0: https://creativecommons.org/licenses/by-nc-sa/4.0/"
email: miguel.pinilla@saldubatech.com
share: true
title: Operation Systems Monitoring and Control
---

## What is an *Operation System*?

> Give some examples

## Key characteristics

- Continuous, Repetitive Operation
- Consume **Materials** and create *Products* in discrete amounts
- May consume other ancillary resources (e.g. energy)

> Black Box view

## Measuring Operations Performance

- Yield
- Throughput
- Sojourn/Lead-Time
- Work In Progress
- Cost
- Utilization

## Queueing Model of Operations

- Arrival
- Start
- Complete
- Departure*

### Little's Law

### Throughput/Lead Time Relationship

### Resource Consumption

### Yield

## The Control Problem

- Goal: Keep the system operating in the *design window* w.r.t.:
  - Throughput, Lead-time, Yield
- Levers

## Additional Notes

### Characteristics/Concepts

- Discrete unit of output: **Job**
- Jobs are produced by performing **Processes**
- Processes are partially ordered sets of **Tasks**
- Tasks are:
  - Discrete (start-end)
  - Parametric
  - Variable/Stochastic

- Tasks are performed by **Stations** which
  - Consume Materials and other resources
  - Have finite *Capacity*
  - Station's behavior has a stochastic component

### Interactions

- Jobs can be successful or fail
- Processes prescribe the (partial) order in which Tasks can be executed.
- A Task execution is possible only when:
  1. Any preceding Task in the process has been completed
  2. A Station that can perform the task is available.
  3. The materials required are available at the station
  4. Other Required Resources are available
- Otherwise, the Task must wait to be performed.

### System "Design Point"

- Some simplifications:
  - Fixed Capacity
  - Yield Independence/constant
  - Linear Costs

- Possible Objectives:
  - Minimize Cost s.t. min Throughput max Lead-time
  - Minimize Lead-Time s.t. min Throughput max Cost
  - Maximize Throughput s.t. max Cost max Lead-Time