---
title: Indicator
excerpt: The definition of an indicator
categories: []
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
| apiVersion | see [metadata](./index.md/#apiVersion) |
| kind | see [metadata](./index.md/#kind) |
| metadata | see [metadata](./inex.md/#metadata) |
| spec | see [spec](./index.md/#spec) |
| spec.from | The date that marks the start of the range that the indicator data relates to. |
| spec.to | The date that marks the end of the range that the indicator data relates to. |
| spec.percent | The percentage of the value defined by the indicaitor labels that relate to this period in time. |