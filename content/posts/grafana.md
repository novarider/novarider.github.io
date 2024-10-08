---
title: "InfluxDB with Graphana"
date: 2024-10-08T22:00:00+01:00
draft: false
---

# The problem

In our home there is a [Loxone smart home server](https://www.loxone.at) which provides HTML endpoints to fetch data and the possibility to create historical data from it. 
Historical data are then served as CSV and XML files, one file per day and measurement point. 
The server also includes a limited visualization of the data, but no possibility to combine or compare the visualizations, 
for example, a merged visualization from two different measurement points.

To easily analyze the produced or recorded data, we need a more sophisticated system. So the technology search started...

# [Grafana](https://grafana.com/grafana/)

Graphana as a visualization tool brings some really nice features with it

  - Many data sources are supported via plugins
  - Great options for visualization
    - Different graphical charts/visualizations
    - Mixing different data sources or visualizations into one common one
  - Possibility to create alarms for the monitored data
  - Create dashboards from the created alarms and graphs/visualizations, which can then can be published

From these points the tools seems perfect for our use case and because it is open source we can run it on our existing server without significant more costs.

## Grafana with an XML data source

So I pulled the [Grafana docker image](https://hub.docker.com/r/grafana/grafana) and spun it up with default options to create a proof of concept. 
And a few seconds later, I started to configure an XML data source with the home server's HTTP endpoint to fetch data from. This worked great and 
in a few minutes, I had a graph with the data.

From that point on, it was easy to import a second dataset from the same server and create a first mixed visualization graph to compare the data.

There, I stumbled over the next problem. The server gives me for everyday a new HTTP endpoint, which makes it not that easy to create a visualization for 
longer than one day into the past. So I decided to find a tech stack to persist my data independently of the server.

# [InfluxDB](https://www.influxdata.com/products/influxdb/) and [Telegraph](https://www.influxdata.com/time-series-platform/telegraf/)

So after taking a look at available plugins on Grafana and some research on the internet, I stumbled over InfluxDB, a database designed for time based data.
Which sounds perfect for the time based sensor data provided by the server. With Telegraph, there is also a worker service to move data from different 
Data sources into the influx database, without creating much overhead, just some configurations.

So I think this is a pretty nice solution, which should work together pretty well without too much overhead. So in the next days I'll try out to set up the whole
stack with the help of docker on my server and will publish the results here on the blog.
