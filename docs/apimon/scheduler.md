Scheduler

Scheduler is python script responsible for scheduling and executing ansible
playbooks. The scheduler periodically scans the repository scenarios. For each
scenario playbook it forks a process, scheduling infinite execution loops of
the scenario. At all times, only one instance of a scenarios is scheduled.
Different scenarios may run concurrently, though. Each new invocation of
a scenario may be delayed by a pause to prevent thrashing or resource
exhaustion. Once the playbook is completed the thread is cleaned up and new
playbook from the queue is added to the free thread. By default scheduler
is setup to 8 parallel threads. 

Scheduler is also responsible for generating job run logs locally,
pushing the logs to Swift, pushing the metrics to Telegraf and
for raising the alerts to Alerta.

The python scheduler and its configuration are hosted on
[github](https://github.com/stackmon/apimon).



