---
title: WebhookCriteria
excerpt: The definition of WebhookCriteria
categories: ["reference", "entities"]
status: published
type: doc
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
| apiVersion | see <g-link to="/reference/entities#apiVersion">APIVersion</g-link> |
| kind | see <g-link to="/reference/entities#kind">Kind</g-link> |
| metadata | see <g-link to="/reference/entities/#metadata">metadata</g-link> |
| spec | see <g-link to="/reference/entities#spec">spec</g-link> |
| spec.url | The url of the webhook. This URL must be able to accept a POST request that contains the entity that caused the event |
| spec.trigger | A collection of properties that must match the incoming event for the webhook to be invoked |
| spec.trigger.event_type | The type of event that this webhook is triggered by. Possible options are `created`, `deleted`, `changed` |
| spec.trigger.api_version | the `api version` of the entity that this webhook is triggered by. |
| spec.trigger.kind | the `kind` of entity that this webhook is triggered by. |
| spec.trigger.lables_selector | The labels that the entity must have in order to trigger this webhook. see <g-link to="/reference/entities#selectors">selectors</g-link> for more information. |