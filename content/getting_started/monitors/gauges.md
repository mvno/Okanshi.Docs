---
title: "Gauges"
date: 2018-10-13T21:54:55+02:00
weight: 2
---

## Description

Gauges are normally returning instantaneous values, but this is only half the truth in Okanshi. Several different gauges exists, but some of the returns aggregated values, like the maxmimum value, minimum value or average values.

The different gauges available are:

| Name | Aggregating | Description |
| ---- | ----------- | ----------- |
| [Gauge](#gauge)| No | Executes a `Func` when polled and returns a instantaneous value |
| [MaxGauge](#maxgauge) | Yes | Keeps track of the maxmimum value since last reset |
| [MinGauge](#mingauge) | Yes | Keeps track of the minimum value since last reset |
| [LongGauge](#longgauge) | No | Reports the last `long` value assigned |
| [DoubleGauge](#doublegauge) | No | Reports the last `double` value assigned |
| [DecimalGauge](#decimalgauge) | No | Reports the last `decimal` value assigned |
| [AverageGauge](#averagegauge) | Yes | Calculate the average value since the last reset |

An aggregated gauge can be used to get the average queue length or the maximum records processed at the same time.

The non-aggregated gauges gives you the last value assigned to the gauge, with the exception of the `Gauge` which gives you an instantaneous value.

It can all be a bit overwhelming, but hopefully the small description and samples below will explain it a bit better.

## How to use?

All gauges, except `Gauge` implements the `IGauge<T>` interface, which provides the `Set(value)` method. This method updates the gauge with the supplied value.

The `Gauge` monitor doesn't implement the interface, instead the `Func` to call when polled, is passed into the constructor.

### Gauge

Executes a `Func` when polled and returns a instantaneous value when polled. This is useful when reporting memory and CPU usage or the current queue length.

```csharp
var gauge = new Gauge(MonitorConfig.Build("GC Total Memory"), () => GC.GetTotalMemory());
```

### MaxGauge

Keeps track of the maxmimum value since last reset. This could be used to determine the maximum queue length or number of HTTP requests within the specifed polling interval.

```csharp
var gauge = new MaxGauge(MonitorConfig.Build("Maximum queue length"));
gauge.Set(1)
gauge.Set(1007)
gauge.Set(8)

// The gauge will return 1007 as the maximum value
```

### MinGauge

Keeps track of the minimum value since last reset. This could be used to determine the minimum queue length or number of concurrent users within the specifed polling interval.

```csharp
var gauge = new MinGauge(MonitorConfig.Build("Minimum queue length"));
gauge.Set(1)
gauge.Set(1007)
gauge.Set(8)

// The gauge will return 1 as the minimum value
```

### LongGauge

As this gauge is not aggregating it will report the last value reported.

```csharp
var gauge = new LongGauge(MonitorConfig.Build("Minimum queue length"));
gauge.Set(0L)
gauge.Set(107L)
gauge.Set(86L)

// The gauge will return 86L when polled
```

### DoubleGauge

As this gauge is not aggregating it will report the last value reported.

```csharp
var gauge = new DoubleGauge(MonitorConfig.Build("Minimum queue length"));
gauge.Set(0.9)
gauge.Set(-1.8)
gauge.Set(7.28)

// The gauge will return 7.28 when polled
```

### DecimalGauge

As this gauge is not aggregating it will report the last value reported.

```csharp
var gauge = new DecimalGauge(MonitorConfig.Build("Minimum queue length"));
gauge.Set(9.788m)
gauge.Set(6786.2799999m)
gauge.Set(1.0m)

// The gauge will return 1.0m when polled
```

### AverageGauge

Keeps track of the minimum value since last reset. This could be used to determine the average queue length or number of HTTP requests within the specifed polling interval.

```csharp
var gauge = new AverageGauge(MonitorConfig.Build("Queue length"));
gauge.Set(4)
gauge.Set(1)
gauge.Set(10)

// The gauge will return 3 as the average value
```