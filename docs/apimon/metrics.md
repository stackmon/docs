The scenarios process generate metrics in two ways:

-   The Ansible playbook internally invokes method calls to **OpenStack SDK
    libraries.** They in turn generate metrics about each API call they do. This
    requires some special configuration in the clouds.yaml file (currently
    exposing metrics into statsd and InfluxDB is supported). For details refer
    to the [config
    documentation](https://docs.openstack.org/openstacksdk/latest/user/guides/stats.html)
    of the OpenStack SDK. The following metrics are captured:
    -   response HTTP code
    -   duration of API call
    -   name of API call
    -   method of API call
    -   service type
-   Ansible plugins may **expose additional metrics** (i.e. whether the overall
    scenario succeed or not) with help of [callback
    plugin](https://github.com/stackmon/apimon/tree/main/apimon/ansible/callback).
    Since sometimes it is not sufficient to know only the timings of each API
    call, Ansible callbacks are utilized to report overall execution time and
    result (whether the scenario succeeded and how long it took). The following
    metrics are captured:
    -   test case
    -   playbook name
    -   environment
    -   action name
    -   result code
    -   result string
    -   service type
    -   state type
    -   total amount of (failed, passed, ignored, skipped tests)

Custom metrics:

In some situations more complex metric generation is required which consists of
execution of multiple tasks in scenario. For such cases the tags parameter is
used. Once the specific tasks in playbook are tagged with some specific metric
name the metrics are calculated as sum of all executed tasks with respective
tag. It's useful in cases where measured metric contains multiple steps to
achieve the desired state of service or service resource. For example boot up of
virtual machine from deployment until succesfull login via SSH.

	tags: ["metric=delete_server"]
	tags: ["az={{ availability_zone }}", "service=compute", "metric=create_server{{ metric_suffix }}"]
