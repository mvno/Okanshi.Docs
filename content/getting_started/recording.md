---
title: "Recording"
date: 2018-10-07T22:42:26+02:00
weight: 20
---

The easiest way to get started recording metrics is to use the static class `OkanshiMonitor`. It provides methods for the different core monitors in Okanshi, and allows you to start recording with a single line of code. The downside of using `OkanshiMonitor` is that it doesn't allow advanced configuration, but more on that later.

```csharp
OkanshiMonitor.Counter("counter_name").Increment();
```

The counter will be created the first time it is used and cache internally for future use.

Overloads exists for providing tags to the monitor

```csharp
OkanshiMonitor.Counter("counter_name", new[] { new Tag("key", "value") })
```