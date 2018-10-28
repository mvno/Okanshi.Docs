---
title: "Windows Performance Counters"
date: 2018-10-28T21:17:11+01:00
weight: 4
---

It is also possible to monitor Windows Performanc Counters in .NET Framework 4.5 or above. This is **not** supported in .NET Core.

The value of the performance counter is polled at the interval specified by the poller.

```csharp
var performanceCounterMonitor = new PerformanceCounterMonitor(MonitorConfig.Build("Available Bytes"), PerformanceCounterConfig.Build("Memory", "Available Bytes"));
```