# 3. SpinOf CloudMon

Date: 2022-01-01

## Status

Accepted

## Context

Sovereign Cloud Stack raised lot of requests for making ApiMon a general
reusable solution that can be integrated into the SCS stack. While APImon is
opensource it is pretty complex to put all pieces together and documentation is
as good as missing

## Decision

Convert regular APImon project into the CloudMon project driven upstream and
allow easier customizations by users.

## Consequences

- Open Telekom Cloud APImon need to be partially reimplemented as upstream
  solution moving OTC specific bits into the "customization" layer

- Documentation for the new CloudMon need to be created

- More of Zuul jobs testing deployment of the CloudMon need to be created.
