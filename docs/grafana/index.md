# Dashboard

[Grafana](https://grafana.com/) is the open source analytics & monitoring
solution. StackMon can use Grafana as a presentation layer for the ApiMon, 
EpMon and CloudMon metrics in various dashboards.

Grafana fullfills most of the StackMon criteria for the visualization of the
metrics:

 - Shows the raw data directly. 
 - Aggregates data. 
 - Defines thresholds
 - Helps to see historical data (i.e. change of the task duration over time). 
 - Easily integrates different types of data streams.

Based on the the environment, source of monitoring, target platform, scoppe of
the services or monitoring type the different dashboards are shown. The
dashboards, tables and graphs are predefined in yaml format at [apimon-tests
repository](https://github.com/stackmon/apimon-tests/tree/main/dashboards) but
can be customized for end user needs.

Grafana uses 2 main data sources for the metrics.
 - TSDB Graphite (OpenStack based metrics)
 - Relational database PostgreSQL (monitoring playbooks test resutls)

** Additionally based on the defined thresholds Grafana can **send alerts 
directly to Alerta**.
