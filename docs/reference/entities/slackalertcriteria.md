---
title: SlackAlertCriteria
excerpt: The definition of SlackAlertCriteria
categories: []
status: published
type: overview
---
# SlackAlertCriteria

A `SlackAlertCrtieria` declaratively defines the data required to send a message to a Slack channel, and the conditions required for the criteria to be used.

## Structure

```yaml
apiVersion: reliably.com/v1
kind: SlackAlertCriteria
metadata:
    labels: {}
    relatedTo: {}
spec:
    objectiveSelector: {}
    channelUrl: <url>
    messageTemplate: <string>
    remainingPercentThreshold: <string>
```

## Properties
| key | description |
|---|---|
| apiVersion | see [metadata](./index.md/#apiVersion) |
| kind | see [metadata](./index.md/#kind) |
| metadata | see [metadata](./inex.md/#metadata) |
| spec | see [spec](./index.md/#spec) |
| spec.objectiveSelector | A selector that describes an objective(s) that this criteria relates to. See [spec](./index.md/#spec) for more information. |
| spec.channelUrl | The URL of the Slack webhook. This URL must begin `https://hooks.slack.com`. |
| spec.messageTemplate | A Golang template string that can be used to dynamically generate the message send to slack. The object passed to the template is an [ObjectiveResult](./objectiveresult.md). See [Golang templates](https://pkg.go.dev/text/template) for more info. |