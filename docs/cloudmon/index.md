# CloudMon manager

Deploying every component of the monitoring is a very tedious task. Especially
dealing with config files in big clusters is not possible without a proper
automation. CloudMon manager is a CLI tool that takes a general configuration
file for the system and an Ansible inventory of all hosts availbale for the
monitoring and performs installation of the components as well as generation of
the correct config files for every component of the system.

Under the hood of the CloudMon manager is again Ansible. It invokes playbooks
through ansible-runner while generating runtime variables and inventories for
deploying specific component. When Ansible is not a best fit, for example when
managing dashboards in Grafana, CloudMon manager process is performing direct
API requests towards Grafana and maintains dashboards and datasources there.

Currently CloudMon manager process is coming with certain expectations and
deployment choices for the system setup. For example as a metric storage
clustered Graphite database is being managed. Manager process is capable to
install Graphite with carbonapi in a cluster mode. Similarly it is capable to
install reference Grafana for easing starting using CloudMon. It is, however,
strongly recommended to review every component and do additional
configurations, or install requeried components via different means as
requested by internal procedures, and take all the necessary security measures.

While doing monitoring of the system it is mandatory to guarantee some form of
high availability of the monitoring itself, otherwise a not working monitoring
can be considered as no problem. Due to that all of the components are being
installed (or expected to be provisioned) in the high availability mode.

## TSDB

GraphiteApp is being chosen as a reliable storage for metrics with easy
horizontal scalability, where metrics can be stored with the chosen replication
factor and desired retention policy. In a cluster setup for monitoring of a big
cloud performance of the graphite web app has shown issues. For that reason
carbonapi, as an alternative implementation of the API using go language, is
being installed. Except of grafana dashboards normally designed for graphite
metrics there is no necessity to use precisely graphite. It is just our choice.
It can be safely replaced with anything else with 2 aspects needed to be
correspondingly adapted:

- StatsD process capturing metrics need to be supporting alternative TSDB and
  configured correspondingly

- Grafana dashboard queries may need to be adapted.

## SQL

Currently PostgreSQL cluster managed by patroni is being supported by CloudMon.
It is capable to install it on the prepared hardware and configure it
correspondingly.

## Grafana

Grafana is there while it is currently standard tool for visualizing metrics.
It is not a requirement.

## SSL Certificates

Nowadays it is unavoidable to use TLS protection for all of the services. Sadly
this is also one of the most challenging things in automating because of
variety of ways to manage those. Due to that CloudMon system assumes all SSL
certificates are available on the hosts and managed outside.

# Project documentation

[CloudMon documentation](https://stackmon-status-dashboard.readthedocs.io/en/latest/)
