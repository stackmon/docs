# ApiMon

ApiMon is a component of the CloudMon that is designed for scheduling and
executing various test scenarios for monitoring of something as complex as a
cloud. It is doing so by taking a configuration matrix or target environments,
monitoring source zones (from where to test the target environment) and a list
of test scenarios from git repositories to be performed.

One major use case is to be executing Ansible playbook, that in example is
trying to provision Server in every availability zone of the selected cloud and
verify that it is possible to connect to the server.

ApiMon was creating for monitoring OpenStack clouds using Ansible OpenStack
modules which relies on the capability of the underlaying OpenStackSDK library
to expose metrics for the performed calls. OpenStackSDK supports StatsD,
InfluxDB and Prometheus metrics, but due to the chosen approach of running
playbook there is no component that can be really queried by Prometheus. As
such only ensuring StatsD metrics produced by the OpenStackSDK library are
being kept and forwarded to the metric storage (Graphite cluster).

Being a flexible component ApiMon is capable to execute not only Ansible
Playbooks, but literaly any executable is providing extra capabilities of doing
things for which there are no Ansible modules available (i.e. invoking python
script using OpenStackSDK directly). With Ansible on it's own having nearly
limitless capability and availability to execute anything else ApiMon can do
pretty much anything. The only expectation is that whatever is being done
produces some form of metric for further analysis and evaluation. Otherwise
there is no sense in monitoring.

In addition to metrics generated and captured by a playbook ApiMon also
captures stdout of the execution and saves this log for additional analysis. If
there is an OpenStack Swift storage available logs are being uploaded there
with a configurable retention policy. Once Sql DB (any supported by sqlalchemy)
is available additional information on the duration and link to log files are
being stored.
