# Openstack SDK

Openstacksdk is a client library for building applications to work with
OpenStack clouds. The project aims to provide a consistent and complete set of
interactions with OpenStack's many services, along with complete documentation,
examples, and tools.

openstacksdk can report statistics on individual API requests/responses in
several different formats.

Note that metrics will be reported only when corresponding client libraries
(statsd for ‘statsd’ reporting, influxdb for influxdb, etc.). If libraries are
not available reporting will be silently ignored.

In StackMon the execution of API related task in ansible playbook monitoring
scenarios rely on the [Python OpenStack
SDK](https://docs.openstack.org/openstacksdk/latest/) which natively generates
the metrics from the triggered API calls. The metrics are sent to statsd and
processed furthermore in graphite.

Openstacksdk python client library is hosted on
[opendev.org](https://opendev.org/openstack/openstacksdk). The details about
statistics reporting using openstacksdk are described on
[openstack.org](https://docs.openstack.org/openstacksdk/latest/user/guides/stats.html).
