# EpMon

Performing extensive tests like provisioning a server is giving a great
coverage, but is usually not something what can be performed very often and
leaves certain gaps on the timescale of monitoring. In order to cover this gap
EpMon component is capable to send GET requests to the given URLs relying on
the API discovery of the OpenStack cloud (perform GET request to /servers or
the compute endpoint). Such requests are cheap and can be performed in the loop
i.e. every 5 seconds. Latency of those calls, as well as the return codes are
being captured and sent to the metrics storage.
