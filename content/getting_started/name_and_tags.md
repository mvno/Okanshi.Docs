---
title: "Name and tags"
date: 2018-10-28T21:03:47+01:00
weight: 40
---

An Okanshi measurement come with both a name and a set of tags, both of which play a role in distinguishing one measurement from another. Think of the name of a measurement as the overal distinguishing component, a key if you will. And think of a tag like an optional subdivision of that measurement that enable you to "slice and dice" you data.

For example, take the measurement named "Request count" that is a counter counting the number of requests our system receives. We can sum our measurements for a time period and know our load. We can then use the tag "servername" to group our measurements so we know about the distribution of load across our cluster. We can then further split our data using the tag "endpoint path" to see within each server what end points are the most active.

Recall that we said we can "slide and dice" data with tags. For example, we can choose to only see the request count pr. endpoint to get an overall overview of our end point traffic disregarding the actual machines they hit. Another useful tag could be an "environment" tag describing whether you are in test, pre-production, production, ...

Had we instead incorporated server name and end point names in the measurement name, we would not be able to do the same kind of dynamic grouping of data.

These were just two examples of how you can utilize names and tags. What tags you best fit your situation is difficult to say, but we can provide a list of inspiration for general useful tags.

* **Computer name**: The name/id of the computer making measurement can identify if a particular machine or hardware is experiencing problems.
* **Environment name**: For example "test" and "production" - enable you to see how things are going in various environments.
* **Request path**: In a web-service context the request path enable you to summarize either on individual end point or globally
* **Request method**: In a web-service context, e.g. GET or POST
* **Unit of measure**: When you cannot determine from the measurement name the unit of measure, and its not a standard unit (e.g. days or seconds) consider applying it as a tag.
