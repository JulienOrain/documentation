---
title: ObjectiveResult
excerpt: The definition of an objectiveResult
categories: ["reference", "entities"]
status: published
type: doc
---
# ObjectiveResult

An `ObjectiveResult` is the result of comparing an <g-link to="/reference/entities/objective/">Objective</g-link> with an <g-link to="/reference/entities/indicator/">Indicator</g-link> 



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
| apiVersion | see <g-link to="/reference/entities#apiVersion">APIVersion</g-link> |
| kind | see <g-link to="/reference/entities#kind">Kind</g-link> |
| metadata | see <g-link to="/reference/entities/#metadata">metadata</g-link> |
| spec | see <g-link to="/reference/entities#spec">spec</g-link> |
| spec.indicatorSelector | The criteria that defines the indicators this result relates to. See <g-link to="/reference/entities#selectors">spec</g-link> for more info. |
| spec.objectivePercent | The percentage defined by the objective that this result is generated from. |
| spec.actualPercent | The percentage defined by the indicator that this result is generated from. |
| spec.remainingPercent | The result of `spec.actualPercent` - `spec.objectivePercent`. |