---
author: Miguel Pinilla
Copyright: (c) Miguel Pinilla, All rights reserved
License: "This work is licensed under the Creative Commons License CC BY-NC-SA 4.0: https://creativecommons.org/licenses/by-nc-sa/4.0/"
email: miguel.pinilla@saldubatech.com
share: "true"
title: Topic Ideas: Measurements and Metrics Topics
---

{{ draftMark }}

!!! note
    Personal Notes, not for distribution

* Motivation: Show the problem that can be formulated as a Measurement Problem. E.g.
  * IOT, Supply Chain Visibility, Control Systems, Fraud Detection, …
* Math helps us be precise about this: Measures
  * What is a Measurement
    * Look at a thing and say something about it
    * Compare a thing to a standard
    * Assign a value from a set to an object through a well defined procedure.
  * Measurements depend on the “set of values” (scale) that is used to do the assignment
    * Categorical Sets: Labeling // Descriptive statistics (counts, mode)
    * Ordered Sets: Ordering // Compare, Median, Percentiles, …
    * Interval: Measure Distances // Difference, Addition, Averages, Variances (not quite Stdev), Errors, …
    * Rational: They have a `True Zero` // ratios, stdev, derivatives, etc…
* Engineering Models allow us to actually interface the world
  * A Measure is intended to assign a value to a property of interest of an object in the world
  * The assignment procedure is an “Observation”
    * Must be repeatable (when applied to the same object and context, it results on same measure)
    * It is performed at a given moment in time (which is usually part of the “context” of the observation)
    * It is usually done through an instrument that implements the measurement procedure
  * Observations can have errors that affect
    * Repeatability of results across multiple Observations (Precision)
    * How closely the resulting measure represents the “ideal” property of the object (Accuracy)
  * Errors:
    * Are due to (a) Instrument imperfections (b) Unavoidable variations of the context or the context or object
    * Can be systemic (bias) or random (noise)
* Instrument Calibration
  * Against reference instruments
  * By repeated observations
  * By adjustment to theoretical behaviors and uncorrelated observations
* Measures happen in time
  * Timestamped: When did it happen
  * Time Series Report
    * Measurement Frequency.
    * Accumulation Interval
    * Reporting Period
  * Bi-Timestamped: When did I know about it: Required for understanding/auditing “non-reversible” actions
* Impact on Systems Engineering
  * Measure vs. Control
  * Big-System Instruments: IOT, Chemical Plants, National Weather System
  * Understand the Information Content of your system
