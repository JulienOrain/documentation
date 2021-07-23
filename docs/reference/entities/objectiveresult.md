---
title: ObjectiveResult
excerpt: The definition of an objectiveResult
categories: []
status: published
type: overview
---
# ObjectiveResult

An `ObjectiveResult` is the result of comparing an [Objective](./objective.md) with an [Indicator](./indicator.md)

## Structure

```yaml
apiVersion: reliablyhq.com/v1
kind: ObjectiveResult
metadata:
    labels: {}
    relatedTo: {}
spec:
    indicatorSelector: {}
    objectivePercent: <number>
    actualPercent: <number>
    remainingPercent: <number>
```

## Properties
| key | description |
|---|---|
| apiVersion | see [metadata](./index.md/#apiVersion) |
| kind | see [metadata](./index.md/#kind) |
| metadata | see [metadata](./inex.md/#metadata) |
| spec | see [spec](./index.md/#spec) |
| spec.indicatorSelector | The criteria that defines the indicators this result relates to. See [spec](./index.md/#selectors) for more info. |
| spec.objectivePercent | The percentage defined by the objective that this result is generated from. |
| spec.actualPercent | The percentage defined by the indicator that this result is generated from. |
| spec.remainingPercent | The result of `spec.actualPercent` - `spec.objectivePercent`. |