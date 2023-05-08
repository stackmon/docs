
# Alerta

Alerta is a component of the **CloudMon** that is designed to integrate
**alerts** from multiple sources. It supports many different standard sources
like Syslog, SNMP, Prometheus, Nagios, Zabbix, etc. Additioanlly any other type
of source using URL request or command line can be integrated as well.

Native functions like **correlation** and **de-duplication** help to manage
thousands of alerts in transparent way and consolidate alerts in proper
categories based on environment, service, resource, failure type, etc.

Alerts displayed on OTC Alerta are generated either by Executor, Scheduler,
EpMon or by Grafana.

 - “**Executor alerts**” focus on playbook results, whether playbook has
   completed or failed.
 - "**EpMon alerts**" focus on query results from endpoint monitoring and detect
   issues like timeouts, 50X errors.
 - “**Grafana alerts**” focus on breaching the defined thresholds. For example
   API response time is higher than defined threshold.

The Zulip API was integrated with Alerta, to send notification of errors/alerts
on zulip stream.

Alerta is a component of the API-Monitoring requiring a proper fail-over. It can
be implemented in different ways with a real load-balancer instance, DNS with
load-balancer, DNS round-robin, etc. We currently do this as a DNS with
round-robin switching between different environments which is accompanied by
HAProxy load balancing distributing the traffic to multiple Alerta instances.
In this case a clustered Alerta setup is using Patroni as a clustered DB in the
backend.

Alerta's Dockerfile as well as Zulip integration plugin are hosted on
[github](https://github.com/opentelekomcloud-infra/alerta).

