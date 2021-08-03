---
title: WebhookCriteria
excerpt: The definition of WebhookCriteria
categories: []
status: published
type: overview
---
# WebhookCriteria

A `WebhookCriteria` declaratively defines the data required to invoke a remote webhook when a certain internal event is received.

## Structure

```yaml
apiVersion: reliably.com/v1
kind: WebhookCriteria
metadata:
    labels: {}
    relatedTo: {}
spec:
    url: <string>
    trigger:
        event_type: <string>
        api_version: <string>
        kind: <string>
        labels_selector: {}
```

## Properties
| key | description |
|---|---|
| apiVersion | see [metadata](./index.md/#apiVersion) |
| kind | see [metadata](./index.md/#kind) |
| metadata | see [metadata](./index.md/#metadata) |
| spec | see [spec](./index.md/#spec) |
| spec.url | The url of the webhook. This URL must be able to accept a POST request that contains the entity that caused the event |
| spec.trigger | A collection of properties that must match the incoming event for the webhook to be invoked |
| spec.trigger.event_type | The type of event that this webhook is triggered by. Possible options are `created`, `deleted`, `changed` |
| spec.trigger.api_version | the `api version` of the entity that this webhook is triggered by. |
| spec.trigger.kind | the `kind` of entity that this webhook is triggered by. |
| spec.trigger.lables_selector | The labels that the entity must have in order to trigger this webhook. see [selectors](./index.md/#selectors) for more information. |