---
title: "Use tags"
date: 2018-10-28T21:28:02+01:00
weight: 20
---

While naming monitors is important, remember you can configure tags that are supplied with all measurements. But what tags to use. The following list may serve you as a list of inspiration. Remember, tags can be used in the consuming system to slice and dice the data. Tags enable to you separate data, but you can always aggregate all data solely based on the name of your measurements.

The list

* **Computer name**: The name/id of the computer making measurement can identify if a particular machine or hardware is experiencing problems.
* **Environment name**: For example "test" and "production" - enable you to see how things are going in various environments.
* **Request path**: In a web-service context the request path enable you to summarize either on individual end point or globally
* **Request method**: In a web-service context, e.g. GET or POST
* **Unit of measure**: When you cannot determine from the measurement name the unit of measure, and its not a standard unit (e.g. days or seconds) consider applying it as a tag.
