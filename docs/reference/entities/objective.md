---
title: Objective
excerpt: The definition of an objective
categories: ["reference", "entities"]
status: published
type: overview
---
# Objective

An `Objective` declaratively defines a single Service Level Objective

## Structure

```yaml
apiVersion: reliablyhq.com/v1
kind: Objective
metadata:
    labels: {}
    relatedTo: {}
spec:
    indicatorSelector: {}
    objectivePercent: <number>
    window: <duration>
```

## Properties
| key | description |
|---|---|
| apiVersion | see <g-link to="/reference/entities#apiVersion">APIVersion</g-link> |
| kind | see <g-link to="/reference/entities#kind">Kind</g-link> |
| metadata | see <g-link to="/reference/entities/#metadata">metadata</g-link> |
| spec | see <g-link to="/reference/entities#spec">spec</g-link> |
| spec.indicatorSelector | see <g-link to="/reference/entities#selectors">selectors</g-link> |
| spec.objectivePercent | The percent required by this objective |
| spec.window | The window of time that should be used to select data that can be used to test the actual state of a system. See [this](https://pkg.go.dev/time#ParseDuration) for more info. |