---
title: Objective
excerpt: The definition of an objective
categories: []
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
| apiVersion | see [metadata](./index.md/#apiVersion) |
| kind | see [metadata](./index.md/#kind) |
| metadata | see [metadata](./inex.md/#metadata) |
| spec | see [spec](./index.md/#spec) |
| spec.indicatorSelector | see [selectors](./index.md/#selectors) |
| spec.objectivePercent | The percent required by this objective |
| spec.window | The window of time that should be used to select data that can be used to test the actual state of a system. See [this](https://pkg.go.dev/time#ParseDuration) for more info. |