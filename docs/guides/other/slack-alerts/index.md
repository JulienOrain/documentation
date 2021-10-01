---
title: Integrating with Slack
excerpt: How to bring Slack into your Reliably ecosystem
categories: ["guides", "other-guides"]
status: published
type: doc
---

# Integrating with Slack

Reliably supports integration with Slack. It is possible to configure Reliably
to send a message to Slack when the budget for a given objective is less than
the threshold set in the alert configuration.

## Example

Create a manifest using the definition <g-link to="/reference/entities/slackalertcriteria/">here</g-link>

### Objective

```yaml
apiVersion: reliably.com/v1
kind: Objective
metadata:
    labels:
        service: my awesome service
        name: error rate is less than 1 percent
spec:
    indicatorSelector:
        category: error_rate
        aws_resource_arn: arn:partition:service:region:account-id:resource-id
    objectivePercent: 1
    window: 1h
```

### Slack Alert Criteria

```yaml
apiVersion: reliably.com/v1
kind: SlackAlertCriteria
metadata:
    Labels:
        name: my slack alert
spec:
    objectiveSelector:
        service: my awesome service
        name: error rate is less than 1 percent
    channelURL: https://hookls.slack.com/some-webhook-url
    messageTemplate: Error rate has been exceeded!
    remainingPercentThreshold: "< 1"
```

In this scenario, when an indicator is sent that matches the **Objective**, the
difference between the actual performance and the objective performance will be
calculated. This value is then used by the **Slack Alert Criteria** to decide if:

1. the criteria matches the objective. In this case it does because the labels
   of the **Objective** match the **SlackAlertCriteria.spec.objectiveSelector**
   parameters.
2. the calculated remaining percent is less than the threshold defined in the
   **SlackAlertCriteria.spec.remainingPercentThreshold**.

If both of these conditions are met then the message template is parsed and a
message is sent to the URL defined in the **SlackAlertCriteria.spec.channelURL**
property.

### Message Templates

Details on how to create a message template can be found <g-link to="/reference/entities/slackalertcriteria/#properties">here</g-link>.

**Example**:

```text
Remaining percent between {{.Metadata.Labels.from}} and {{.Metadata.Labels.to}} was {{.Spec.RemainingPercent}}%, which is below the alert threshold of 10%
```
