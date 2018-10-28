---
title: "Monitors"
date: 2018-10-07T22:53:49+02:00
weight: 30
---

Okanshi has a couple of different monitor types, divided into the following categories:

* Gauges
* Counters
* Timers

Where a "gauge" is something that returns its most present value, a "counter" is something you increment and a "timer", is the time taken for some chunk of code to execute. At its heart, what Okanshi does, is to aggregate data around these three concepts. Data is aggregated in order for the information load to be manageable both in terms of collection, transmission to a central storage and the following indexing.

The three monitors represents the fundamentals to monitoring. And thus it is not uncommon to see these monitors combined into larger and more complex monitors. In fact, Okanshi is shipping such monitors itself. Why do we need to combine monitors? Remember that values from Okanshi are aggregated values. A measurement from a monitor may stem from possibly thousands of measurements. And so, it may be useful to operate on slightly more than just a single aggregated value.

An example from the trenches: You have a service level agreement to respond to request within 500 ms, and with Okanshi you measure the average time taken to be 400 ms. Are you in the clear? How many times could you have response times above 500 ms and still have an average of 400 ms? The answer is that you can't tell using the simples timer monitor provided in Okanshi. But you can turn to more advanced timers to help you out.

At other times, the simplest readings more than suffice. It depends on a lot of factors. On factor being that your average response time is 10 ms and you maximum response time is 50 ms. Another factor may be that you do not have an explicit SLA with your online users, but you'd like to track long term trends of the user experience and identify releases that particular hurt performance. Do you want automated alarming? Identify critical situations where something is about to go wrong or has gone wrong without the service has crashed?

We consider the art of measuring a fine art. The relevancy of measurements depends on how what you want to do with your results. Gaining an understanding of what you want to do with you data is often an interactive process:

1. You measure data,
1. evaluate the data and its uses,
1. figure out you need to cover new situations or is missing data,
1. you extend the monitoring
1. goto 1.

Also you'll find not all code and not all services needs be treated the same. They have different characteristics, risk profiles etc. that make it relevant to do different kinds of measurements. Hence the iterative process stated above.

Starting with Okanshi, it's perfectly fine if you are unsure on how exactly you want to measure. Likewise, it is just as OK to have a very thorough understanding of what you want to measure, only to get a lot smarter once you see the results.

A monitor is normally reset between each poll, but some monitors exists that are not reset between polls.

The following monitors are provided in the core:

| Type    | Description |
| ------- | ----------- |
| [Counter](counters/#counter) | Allows you to track how many times something has happened, for example the number of HTTP requests. It is an atomic 64-bit integer which can be incremented. |
| [DoubleCounter](counters/#doubelcounter) | An atomic double-precision floating-point counter. |
| [CumulativeCounter](counters/#cumulative_counter) | An ever increasing atomic 64-bit counter. |
| [Gauge](gauges/#gauge) | A Gauge is simply an action that returns an instantaneous measure of a value, for example memory usage. |
| [MaxGauge](gauges/#maxgauge) | A Gauge that keeps track of the maximum value seen since the last poll. |
| [MinGauge](gauges/#mingauge) | A Gauge that keeps track of the minimum value seen since the last poll. |
| [LongGauge](gauges/#longgauge) | A Gauge reporting the last `long` value provided when polled. |
| [DoubleGauge](gauges/#doublegauge) | A Gauge reporting the last `double` value provided when polled. |
| [DecimalGauge](gauges/#decimalgauge) | A Gauge reporting the last `decimal` value provided when polled. |
| [AverageGauge](gauges/#averagegauge) | A Gauge  reporting the average of all the values provided since the last poll. |
| [Timer](/getting_started/monitors/timer) | A Timer is a combination of a Maxgauge, MinGauge, AverageGauge and two Counters, allowing you to measure the duration of an event and provide the maximum duration, minimum duration, average duration, total duration and the number of events since the last poll. |