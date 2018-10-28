---
title: "Timers"
date: 2018-10-07T23:13:57+02:00
weight: 3
---

Timers measures the time it takes to execute a function.

All timers can be instantiated directly or, declared and used through the static `OkanshiMonitor` class.

All timers also support "manual" timing, that are stopped manually instead of passing a `Func` or `Action`. Example:

```csharp
var timer = OkanshiMonitor.Timer("Query time", TimeSpan.FromSeconds(1)).Start()
Thread.Sleep(500);
timer.Stop(); // When stopped the timing is registered
```

The following timers exists the Okanshi core:

* [Timer](#timer)
* [SlaTimer](#slatimer)

## How to use?

All timers implements the interface `ITimer`, meaning they all are used to same way.

## Timer

This is a simple timer that, within a specified interval, measures:

* The execution time of a function,
* Tracks the minimum and maximum time of the function call
* The number of times the function was called
* The total time of the all calls in the specified step
* The rate of the calls (the number of calls per second)

```csharp
var timer = new Timer(MonitorConfig.Build("counter_name"));

// Time an Action
timer.Record(() => Thread.Sleep(500));

// Time a Func
var result = timer.Record(() => {
    Thread.Sleep(500);
    return 100;
});
```

## SlaTimer

A service-level agreement (SLA) is a commitment between a service provider and a client. For example, the service provider promise to respond to a request within an agreed amount of time.

A SLA-Timer is a special timer, that keeps track of your SLA's and whether they are honored. The SLA-Timer is different than a timer in that it measures strictly against the SLA, whereas the Timer operate on averages. If your performance characteristics are such that you are always doing very good or very bad, a normal timer can be used instead of the SLA-timer, since the average will suffice.

The timer implements two timers one for registrations below the SLA and one above. Each timer provides the following data "average", "total time", "count", "min" and "max". We keep track of both executions below the SLA and above. The reason is, when things are going bad we want to know how bad we are doing. By tracking timings below our SLA we can see if we get dangerously close to our SLA, it also enable us to better understand the periods where we break our SLA by knowing how "business as usual" looks like.

```csharp
var timer = new SlaTimer(MonitorConfig.Build("counter_name"), TimeSpan.FromSeconds(30));

// Time an Action
timer.Record(() => Thread.Sleep(500));

// Time a Func
var result = timer.Record(() => {
    Thread.Sleep(500);
    return 100;
});
```
