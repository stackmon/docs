Scheduler

Scheduler is python based tool responsible for scheduling test scenarios by
submitting execution requests towards executors. The scheduler periodically
scans git repositories with scenarios. For each scenario playbook it evaluates
necessity of the execution in certain environment and places job request. At
all times, only one instance of a scenarios is scheduled.  Different scenarios
may run concurrently, though. Each new invocation of a scenario may be delayed
by a pause to prevent thrashing or resource exhaustion.

The python scheduler and its configuration are hosted on
[github](https://github.com/stackmon/apimon).
