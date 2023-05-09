# graphite

 [Graphite](https://graphiteapp.org/) is an open-source enterprise-ready
 time-series database. ApiMon, EpMon, and CloudMon data are stored in the
 clustered Graphite TSDB. Metrics emitted by the processes are gathered in the
 row of statsd processes which aggregate metrics to 10s precision.

General storage retention policy for the metrics is applied by the
[https://raw.githubusercontent.com/stackmon/cloudmon/main/cloudmon/ansible/project/roles/graphite/templates/storage-schemas.conf.j2](https://raw.githubusercontent.com/stackmon/cloudmon/main/cloudmon/ansible/project/roles/graphite/templates/storage-schemas.conf.j2)
and currently evals to "10s:6h,1m:6d,10m:3y"

All metrics are under "stats" namespace:

Under "stats" there are following important metric types:

-   counters
-   timers
-   gauges

Counters and timers have following subbranches:

-   apimon.metric → specific apimon metrics not gathered by the OpenStack API
    methods
-   openstack.api → pure API request metrics

Every section has further following branches:

-   environment name (production_regA, production_regB, etc)
    -   monitoring location (production_regA, awx) - specification of the
        environment from which the metric is gathered


##### openstack.api:

OpenStack metrics branch is structured as following:

-   service (normally service_type from the service catalog, but sometimes differs slightly)
    -   request method (GET/POST/DELETE/PUT)
        -   resource (service resource, i.e. server, keypair, volume, etc). Subresources are joined with "_" (i.e. cluster_nodes)
            -   response code - received response code
                -   count/upper/lower/mean/etc - timer specific metrics (available only under stats.timers.openstack.api.$environment.$zone.$service.$request_method.$resource.$status_code.{count,mean,upper,*})
                -   count/rate - counter specific metrics (available only under stats.counters.openstack.api.$environment.$zone.$service.$request_method.$resource.$status_code.{count,mean,upper,*})
            -   attempted - counter for the attempted requests (only for counters)
            -   failed - counter of failed requests (not received response, connection problems, etc) (only for counters)
            -   passed - counter of requests receiving any response back (only for counters)

  
##### apimon.metric:

-   metric name (i.e. create_cce_cluster, delete_volume_eu-de-01, etc) - complex metrics branch
    -   attempted/failed/failedignored/passed/skipped - counters for the corresponding operation results (this branch element represents status of the corresponding ansible task)
        -   $az - some metrics would have availability zone for the operation on that level. Since this info is not always available this is a varying path
-   curl - subtree for the curl type of metrics
    -   $name - short name of the host to be checked

  
-   stats.timers.apimon.metric.$environment.$zone.**csm_lb_timings**.{public,private}.{http,https,tcp}.$az.__VALUE__ - timer values for the loadbalancer test
-   stats.counters.apimon.metric.$environment.$zone.**csm_lb_timings**.{public,private}.{http,https,tcp}.$az.{attempted,passed,failed} - counter values for the loadbalancer test
-   stats.timers.apimon.metric.$environment.$zone.**curl**.$host.{passed,failed}.__VALUE__ - timer values for the curl test
-   stats.counters.apimon.metric.$environment.$zone.**curl**.$host.{attempted,passed,failed} - counter values for the curl test
-   stats.timers.apimon.metric.$environment.$zone.**dns**.$ns_name.$host - timer values for the NS lookup test. $ns_name is the DNS servers used to query the records
-   stats.counters.apimon.metric.$environment.$zone.**dns**.$ns_name.$host.{attempted,passed,failed} - counter values for the NS lookup test
