---
title: "Observers"
date: 2018-10-28T21:20:57+01:00
weight: 50
---

Observers are used to store Okanshi metrics, this can be in-memory or by sending it to a database. An observer storing metrics in-memory is included in the Okanshi package.

An observer to send metrics to InfluxDB is provided through another NuGet package called, Okanshi.InfluxDBObserver.

## Observer setup

Setting up an observer is easy:

```csharp
var observer = new MemoryMetricObserver(new MetricMonitorRegistryPoller(DefaultMonitorRegistry.Instance, pollingInterval, collectMetricsOnProcessExit), numberOfSamplesToStore)
```

This observer stores metrics in-memory using a poller getting data from the default monitor registry.

## Creating you own observer

You can create your own observers easily as shown in the following example that not only prints to the screen but does some processing first:

```csharp
class MyObserver : IMetricObserver
{
    public MyObserver(IMetricPoller poller)
    {
        poller.RegisterObserver(Update);
    }

    public async Task Update(IEnumerable<Metric> metrics)
    {
        var msg = JsonConvert.SerializeToJson(metrics);
        Console.WriteLine($"sending info to MyLegacySystem<tm> '{msg}'");
    }

    public void Dispose()
    { }
}
```

To set up this particular observer we can use the following code. It sets up some business logic that is timed.

```csharp
class Program
{
    static void Main(string[] args)
    {
        var poller = new MetricMonitorRegistryPoller(DefaultMonitorRegistry.Instance, interval: TimeSpan.FromSeconds(2));
        var observer = new MyObserver(poller);

        BusinessLogic();
    }

    private static void BusinessLogic()
    {
        while (true)
        {
            OkanshiMonitor.Timer("send").Record(() =>
            {
                Thread.Sleep(TimeSpan.FromMilliseconds(200));  // simulate business stuff...
            });
        }
    }
}
```
