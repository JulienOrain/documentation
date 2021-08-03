---
title: Registering a Webhook
excerpt: ReliablyHQ can invoke a webhook when certain events occur. Here's how to do it.
categories: ["guides", "slo"]
status: published
type: doc
---

# Registering a Webhook

Webhook registration is done by submitting a `WebhookCriteria` manifest to ReliablyHQ. This manifest contains the criteria needed to match an entity to your requirements, and then invoke a URL.

An example of the manifest can be found [here](../../../reference/entities/webhookcriteria.md).

The payload sent to the webhook is the entity that triggered the event.

### Webhook requirements

* The webhook URL must be available to the public internet.
* The webhook URL must be able to accept a `POST` request.

## Guide

### 1. Create a manifest

A webhook that is triggered when an `ObjectiveResult` that has a label `service:my awesome service` is created should look like this:

*webhook.yaml*
```yaml
apiVersion: reliably.com/v1
kind: WebhookCriteria
metadata:
    labels:
        name: my awesome webhook
        service: my awesome service
spec:
    url: https://myurl.org
    trigger:
        event_type: created
        api_version: reliably.com/v1
        kind: ObjectiveResult
        labels_selector:
            service: my awesome service
```

### 2. Send the manifest to ReliablyHQ
```
$ reliably slo sync -m webhook.yaml
```

## Context information

Information about the event and the context that created it is added to the request headers. You can use these request headers to aid in your processing, and to associate them back to ReliablyHQ.

| header | description |
|---|---|
| x-reliablyhq-event-type | The type of the event that caused the webhook to be invoked. |
| x-reliablyhq-event-created-at | The time (in ISO format) that this event was created. |
| x-reliablyhq-entity-kind | The kind of entity that triggered this webhook invocation. |
| x-reliablyhq-entity-api-version | The API Version of the entity that triggered this webhook invocation. |
| x-correlation-id | A string that is associated with the context that this invocation came from. This is useful for debugging and should be included in any support requests you make. |

## Coming Soon
* Webhooks will be required to use the HTTPS protocol, with a valid SSL certificate.
* Webhook payload verification using the `sign` capability of [nacl](https://nacl.cr.yp.to/sign.html).

## Reference

[webhookCriteria](../../../reference/entities/webhookcriteria.md)