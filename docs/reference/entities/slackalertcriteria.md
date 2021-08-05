---
title: SlackAlertCriteria
excerpt: The definition of SlackAlertCriteria
categories: ["reference", "entities"]
status: published
type: doc
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
| apiVersion | see <g-link to="/reference/entities#apiVersion">APIVersion</g-link> |
| kind | see <g-link to="/reference/entities#kind">Kind</g-link> |
| metadata | see <g-link to="/reference/entities/#metadata">metadata</g-link> |
| spec | see <g-link to="/reference/entities#spec">spec</g-link> |
| spec.indicatorSelector | The criteria that defines the indicators this result relates to. See <g-link to="/reference/entities#selectors">spec</g-link> for more info. |
| spec.channelUrl | The URL of the Slack webhook. This URL must begin with `https://hooks.slack.com`. |
| spec.messageTemplate | A Golang template string that can be used to dynamically generate the message send to slack. The object passed to the template is an <g-link to="/reference/entities/objectiveresult/">ObjectiveResult</g-link>. See [Golang templates](https://pkg.go.dev/text/template) for more info. |