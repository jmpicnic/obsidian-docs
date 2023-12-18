---
author: Miguel Pinilla
Copyright: (c) Miguel Pinilla, All rights reserved
License: "This work is licensed under the Creative Commons License CC BY-NC-SA 4.0: https://creativecommons.org/licenses/by-nc-sa/4.0/"
email: miguel.pinilla@saldubatech.com
share: "true"
title: Measurements and Metrics
---

## Key Concepts to Define Metrics

1. **Measurement**: A quantitative value observed on a resource at an
    instant in time and associated with a label. Measurements provide a
    snapshot of a resource\'s attribute at a specific moment.

2. **Measurement Interval**: The duration of time between two
    consecutive measurements. It represents the time span between
    successive observations of a resource\'s attribute.

3. **Measurement Period:** The time interval between two measurements.
    It may be a constant determined by the measurement process used, or
    determined by events triggered by the resource itself.

4. **Sampling Frequency**: The rate at which measurements are taken
    within a specific time frame. It is the inverse of the measurement
    period and determines data granularity.

5. **Metric**: A statistical value calculated over a series of
    measurements, offering insights into the resource\'s characteristics
    or behavior over time. Metrics summarize data and aid in
    decision-making.

6. **Metric Calculation Time:** The point in time when a Metric is
    computed.

7. **Metric Calculation Period**: An integer number of measurement
    periods during which a metric is calculated. It establishes a
    consistent time frame for metric analysis. The calculation period is
    defined relative to the Calculation point and it can be lagging (the
    calculation time is at the end of the period), leading (the
    calculation is at the beginning of the period) or other alternatives
    (e.g. centered). Note that for real time computed metrics, the most
    common are where the calculation time is lagging the calculation
    period. E.g. the inflation rate is measured over the last 12 months.

8. **Report Point**: A data point consisting of an instant of time and
    the corresponding metric value, calculated over the metric
    calculation period. The instant of time corresponds to the metric
    calculation time.

9. **Report:** A collection of report points with consecutive metric
    calculation periods. Reports organize data points to illustrate how
    metrics evolve over time.

10. **Reporting Period**: The time between the end of the first metric
    calculation period and the end of the last calculation period in a
    report. It defines the overall time frame covered by the report\'s
    data and insights.

## Additional Concepts

1. **Accuracy and Precision:** Accuracy refers to how closely a
    measurement aligns with the true or accepted value of the attribute
    being measured. Precision refers to the degree of consistency and
    reproducibility in repeated measurements. Both accuracy and
    precision are essential for reliable measurements.

2. **Validity and Reliability**: Validity refers to the extent to which
    a measurement accurately represents the intended attribute or
    characteristic. Reliability refers to the consistency and stability
    of measurements over repeated trials. Valid and reliable
    measurements are essential for meaningful analysis.

3. **Scale of Measurement**: This refers to the level of measurement
    used for a particular attribute. Scales can be nominal
    (categorical), ordinal (ranked), interval (equal intervals between
    values), or ratio (absolute zero point). The scale influences the
    types of statistical analyses that can be performed.

4. **Normalization**: Normalizing data involves adjusting measurements
    to a standard scale, often between 0 and 1. This is useful when
    comparing measurements with different units or ranges, allowing for
    fair comparisons.

5. **Outliers**: Outliers are data points that significantly deviate
    from the rest of the dataset. They can impact the accuracy of
    calculated metrics and should be carefully considered in analysis.

6. **Bias**: Bias refers to a systematic error that consistently skews
    measurements in a certain direction. It can arise from measurement
    instruments, data collection methods, or other factors.

7. **Sampling Methods**: Different techniques for selecting a subset
    (sample) from a larger population for measurement. Proper sampling
    methods are crucial for obtaining representative data.

8. **Statistical Significance**: This concept is used to determine if
    the differences or patterns observed in a dataset are likely to be
    genuine and not due to random chance.

9. **Data Visualization:** Techniques for representing data visually,
    such as graphs and charts, to make patterns and trends more
    accessible.

10. **Confounding Variables**: These are variables that are not part of
    the main study but can influence the observed relationship between
    variables being studied.

These concepts are important for a comprehensive understanding of
measurement, data analysis, and the creation of meaningful reports and
insights. They play a crucial role in ensuring the accuracy,
reliability, and validity of measurements and the metrics derived from
them.

## Application to API Endpoint Latency Performance

### Measurement

Latency measurements are based on start and end events for an API call
with the following information:

```json
{
    call_id     : UUID,
    time        : Timestamp,
    event       : [start, end,
    result_code : HttpCode"
}
```

The latency measurement is the difference between the end and start
timestamps of the same call, assigned at the timestamp of the end event.
The measurement is taken at each "end" even. The result code, present
only on **end** may be used to select subsets of measurements for
specialized metrics.

```json
{
    call_id     : UUID,
    start_time  : Timestamp,
    end_time    : Timestamp,
    latency     : Long,
    result_code : HttpCode
}
```

### Measurement Period/Sampling Frequency

In this case it is not a constant interval, but the difference between the times of two consecutive start events. It can be represented as:

```json
{
    call_id             : UUID,
    previous_call_id    : UUID,
    last_start_time     : Timestamp,
    current_start_time  : Timestamp,
    inter_arrival_time  : Long
}
```

### Metric

There are several metrics of interest all referring to the Metric
Calculation Period

1. Average and P90 value of the latency values for measurements with a
    successful result code.

2. Number of Measurements with a successful result code

3. Yield: An additional, derived metric is the total number of
    measurements over the number of measurements with a successful
    result code.

4. Total Throughput: Total number of Measurements per unit time

5. Successful Throughput: Number of successful calls per unit time

6. The average of inter-arrival times.

### Metric Calculation Time

In high traffic applications it is not practical to compute the metric
at the same time as each measurement is taken, but rather do it at
regular times. A typical use is to have calculation times at each hour
or simple fractions of an hour (30', 15', 5' or 1')

### Metric Calculation Period

The metric calculation period needs to be long enough to get a
representative number of measurements in it so that the defined metrics
have statistical significance. It should be no lower than 50 times the
expected measurement interval average and preferably at least 100 times
longer. In any case, it should be equal or longer than the interval
between calculation times to avoid skipping any measurements. It will be
a lagging metric, meaning that it will be computed with the measurements
available at the calculation time.

To put it all together, the metrics will be calculated each hour taking
into account a lagging period of time that includes a reasonably large
number of calls.

### Report Point

A report point is generated as :

```json
{
    metric_time                 : Timestamp,
    metric_period               : Long,
    number_of_measurements      : Long,
    average_latency             : Decimal,
    p90_latency                 : Decimal,
    yield                       : Decimal,
    total_call_number           : Long,
    successful_call_number      : Long,
    average_inter_arrival_time  : Long
}
```

### Reports

The report should show the value of the metrics in a line chart with the
horizontal axis representing time for the current Reporting Period.

In the chart, two lines should be represented:

1. The line for the metric value during the current reporting period.

2. The line for the metric value during a reference reporting period in
    the past (e.g. 1 year or 1 quarter ago)

### Reporting Period

A typical reporting period is 30 days trailing.
