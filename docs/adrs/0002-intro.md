# 2. Need for StackMon

* Status: proposed
* Deciders: [list everyone involved in the decision] <!-- optional -->
* Date: 2020-XX-XX

Technical Story: [description | ticket/issue URL] <!-- optional -->

## Context and Problem Statement

There are multiple existing solution to monitor certain systems, but so far there 
is nothing that can cover complexity of monitoring cloud. Such system involves very
complex component relations and can not be normally monitored by simple metrics.

## Decision Drivers <!-- optional -->

* Public Cloud provider need to be able to see and measure quality of service it delivers

## Considered Options

* Just use Prometheus
* Use RefStack/tempest
* ...

## Decision Outcome

It is decided that introduction of a monitoring stack specialized on monitoring of OpenStack clouds should be created.

Stack should be implementing/using following components

* Grafana for visualization of captured metrics
* Graphite for storing metrics (in HA mode)
* Ansible playbooks describe testing scenarios representic user load (usage scenarios)
* Scheduler component ensuring every existing ansible playbook is being permamently executed in the loop (with certain total load throttling)


## Pros and Cons of the Options

### Prometheus

* Good, because it is considered as de-facto standard
* Bad, because user load in the public cloud is about events and not metrics (what is a metric for i.e. server provisioning)
* Bad, because we need more details about certain tests (i.e. server provisioning started to fail, so need to have also logs)

### RefStack/Tempest

* Good, because certain tests are already defined
* Bad, because hard to understand by a regular user/op - requires deep developer skils


## Links <!-- optional -->

* [Link type] [Link to ADR] <!-- example: Refined by [ADR-0005](0005-example.md) -->
* … <!-- numbers of links can vary -->
