# Status Dashboard

Once system is monitoried there might be a desire to have a status dashboard
that uses monitoring data. Being something like a public cloud puts certain
expectations on the features and design of the status dashboard. Fulfilling
those requirements in existing dashboards is not always easy therefore some
tiny, but extensible dashboard is being created. It follows the same pattern
with alternative solutions and consists of 2 major items: components and
incidents.

## Component

Component is an entity with certain attributes (in example a compute service in
region A and compute service in region B if those are physically separated).
This entity represent certain service and is monitored.

## Incident

An incident is an obstacle for the service to do what it should do. Every
incident affects some components, has some effect degree (minor incident,
outage, maintenance), information on begin and end and history of changes.

Absence of an open (empty end date) incident for the service is normally
treated as "the service is up and running".

## Workflow

Status dashboard is only a place for visualization of incidents. It is not
doing any monitoring on it's own, but rather expects that monitoring system
will raise an incident once certain conditions are met. So once certain
criteria are fulfilled monitoring system invokes API of the status dashboard
and opens new incident (or course not if the one for the service is already
open)

In order to avoid flaky situations and to force platform operations team to
treat incidents correspondingly incidents are never closed automatically, but
enforces a human interaction with proper communication.

There is a need to also have certain system maintenances. In order to avoid
incidents being reported during this timeframe a special incident with type
maintenance can be opened ba human in advance.
