---
title: "Performance tuning"
date: 2018-10-28T21:30:44+01:00
weight: 40
---

When using the static class `OkanshiMonitor` there are two ways to instantiate/get hold of a monitor.

```csharp
class SlowUsage
{
    void Foo()
    {
       OkanshiMonitor.Gauge("xxx").SetValue(...)
    }
}

class FastUsage
{
    static IGauge xxx = OkanshiMonitor.Gauge("xxx")

    void Foo()
    {
      xxx.SetValue(...)
    }
}
```

The first way of getting instances is much more lightweigh syntax-wise. And it may be a good way to get up and running. But there is an overhead, in that Okanshi has to do a lookup in its internal cache. Thus the second approach may be preferable if you are fetching the same monitor several times a second.