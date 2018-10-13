---
title: "Counters"
date: 2018-10-13T21:40:44+02:00
weight: 1
---

## Description

Counters are the most basic monitor of them all. They allow you to increment the value each time it is called.

It can be used in a lot of scenarios, like how many HTTP request are made to the server, the number times an action is performed and more.

Out of the box Okanshi provides three different counters:

* [Counter](#counter)
* [DoubleCounter](#doublecounter)
* [CumulativeCounter](#cumulativecounter)

## How to use?

All counters implements the interface `ICounter`, meaning they all are used to same way.

### Counter

Allows you to track how many times something has happened, for example the number of HTTP requests. It is an atomic 64-bit integer which can be incremented

```csharp
var counter = new Counter(MonitorConfig.Build("counter_name"));

// Increment the counter by one
counter.Increment();

// Increment the counter by a user supplied value
counter.Increment(156);
```

### DoubleCounter

An atomic double-precision floating-point counter.

```csharp
var counter = new DoubleCounter(MonitorConfig.Build("counter_name"));

// Increment the counter by one
counter.Increment();

// Increment the counter by a user supplied value
counter.Increment(1.7);
```

### CumulativeCounter

An increasing atomic 64-bit counter that never are reset.

```csharp
var counter = new CumulativeCounter(MonitorConfig.Build("counter_name"));

// Increment the counter by one
counter.Increment();

// Increment the counter by a user supplied value
counter.Increment(15);
```