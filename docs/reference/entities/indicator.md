---
title: Indicator
excerpt: The definition of an indicator
categories: ["reference", "entities"]
status: published
type: overview
---
# Indicator

An `Indicator` declaratively defines a single Service Level Indicator

## Structure

```yaml
apiVersion: reliablyhq.com/v1
kind: Indicator
metadata:
    labels: {}
spec:
    from: <date>
    to: <date>
    percent: <number>
```

## Properties
| key | description |
|---|---|
| apiVersion | see <g-link to="/reference/entities#apiVersion">APIVersion</g-link> |
| kind | see <g-link to="/reference/entities#kind">Kind</g-link> |
| metadata | see <g-link to="/reference/entities/#metadata">metadata</g-link> |
| spec | see <g-link to="/reference/entities#spec">spec</g-link> |
| spec.from | The date that marks the start of the range that the indicator data relates to. |
| spec.to | The date that marks the end of the range that the indicator data relates to. |
| spec.percent | The percentage of the value defined by the indicaitor labels that relate to this period in time. |