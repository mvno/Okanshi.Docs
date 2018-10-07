---
title: "Monitors"
date: 2018-10-07T22:53:49+02:00
weight: 30
---

Okanshi includes various types of monitors, each providing their own usefulness depending on the measurement tracked.

A monitor is normally reset between each poll, but some monitors exists that are not reset between polls.

The following monitors are provided in the core:

| Type    | Description |
| ------- | ----------- |
| [Counter](/getting_started/monitors/counter) | Allows you to track how many times something has happened, for example the number of HTTP requests. It is an atomic 64-bit integer which can be incremented. |
| [DoubleCounter](/getting_started/monitors/double_counter) | An atomic double-precision floating-point couner. |
| [CumulativeCounter](/getting_started/monitors/cumulative_counter) | An ever increasing atomic 64-bit counter. |
| [Gauge](/getting_started/monitors/gauge) | A Gauge is simply an action that returns an instantaneous measure of a value, for example memory usage. |
| [MaxGauge](/getting_started/monitors/max_gauge) | A Gauge that keeps track of the maximum value seen since the last poll. |
| [MinGauge](/getting_started/monitors/min_gauge) | A Gauge that keeps track of the minimum value seen since the last poll. |
| [LongGauge](/getting_started/monitors/long_gauge) | A Gauge reporting the last `long` value provided when polled. |
| [DoubleGauge](/getting_started/monitors/double_gauge) | A Gauge reporting the last `double` value provided when polled. |
| [DecimalGauge](/getting_started/monitors/decimal_gauge) | A Gauge reporting the last `decimal` value provided when polled. |
| [AverageGauge](/getting_started/monitors/average_gauge) | A Gauge  reporting the average of all the values provided since the last poll. |
| [Timer](/getting_started/monitors/timer) | A Timer is a combination of a Maxgauge, MinGauge, AverageGauge and two Counters, allowing you to measure the duration of an event and provide the maximum duration, minimum duration, average duration, total duration and the number of events since the last poll. |