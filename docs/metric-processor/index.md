# Metrics processor

When monitoring cloud it is not unusual to have a variety of metrics types
(latencies, status codes, rates). Visualizing overall state of the service
based on those metrics is not an easy task in this case. Even simply
identifying whether single metric is showing "good" or "bad" is not trivial.

It is desired to have something like a semaphore to visualize overall "health"
of the component (green - up and running, yellow - there are some issues, red -
complete outage). Depending on the used TSDB there might be no way to do this
at all.

Looking at the challenge from bottom to top it is possible to make few
conclusions:

- service can be considered as having issues if metric `A` and/or `B` is
  showing issues.
- metric `X` is showing issues if the certain TSDB function over the value(s)
  is under/above/equal some threshold.

Exactly this is happening in the metric processor (but surely in the proper
order). First there is a set of TSDB queries defined and for every query the
result is compared against a certain threshold. Those build up a so called
"flag" metrics (latency is too high, error rate too high, success rate too low,
etc).  Further combining few "flags" it is possible to make an assumption
whether service is running without issues, degraded or having a complete
outage.

Metric processor currently serves 2 indenpendent needs:
- convert series of raw metrics of different types into flags and single
  semaphore-like metrics (which can be visualized i.e. in Grafana)
- inform status dashboard once certain component status is not healthy.

Metrics processor is rust based application hosted on
[github](https://github.com/stackmon/metrics-processor)
