---
title: Define and observe your reliability
excerpt: Define SLOs, push SLIs, and view your reports.
categories: ["getting-started"]
status: published
type: doc
---

import Setup from '~/components/Setup.vue'
import Tab from '~/components/Tab.vue'
import Tabs from '~/components/Tabs.vue'
import AsciiPlayer from '~/components/AsciiPlayer.vue'
import CopyToClipboard from '~/components/MarkdownCopyToClipboard.vue'

# Define and observe your reliability

In this section you will learn how to define and observe your reliability by implementing Service Level Objectives with Reliably. After an initial setup with the CLI, you will define your Objectives and Indicators, push Indicator instances, and view a report. This will enable you to take an SLO-oriented approach to reliability.

<!-- TODO: A sandox option notice, when that's finished, should be noted/linked somehow without disturbing the flow. -->

<Setup />

## Define your Objectives

To get started, you will generate a manifest file defining your Objectives and an Indicator selector for each. These two entities will allow you to define what good looks like for your system from the perspective of your users. In order to do this, you first need to determine your data provider for the resources you wish to target. This may be the cloud platform which contains the resources such as AWS or GCP, or alternatively a monitoring service such as Datadog.

:::note Note
If you would prefer to start with a sandboxed deployment, instead of your own resources, follow the instructions of deployment for your preferred platform below and then return to this section.

[AWS](https://github.com/reliablyhq/walkthrough-slo-capability-aws) / [GCP](https://github.com/reliablyhq/walkthrough-slo-capability-gcp)
:::

<Tabs>
<Tab name="AWS" selected="true">

### AWS

To get started you will need:

1. An AWS account with access to CloudWatch
2. A Load Balancer or API Gateway deployed
3. A local AWS [credentials file configured](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html).

On your working directory, define your Objectives and Indicator selectors with:

```console
reliably slo init
```

<CopyToClipboard />

When you're done, the CLI will confirm your manifest has been successfully created in your working directory.

```reliably
<span class="token green">✓</span> Your manifests has been saved to ./reliably.yaml
````

You must then sync your manifest with Reliably's API:

```console
reliably slo sync
```

<CopyToClipboard />

</Tab>
<Tab name="GCP">

### GCP

To get started you will need:

1. A GCP account with access to the Monitoring API
2. A Load Balancer deployed
3. Authorise your environment with [gcloud auth](https://cloud.google.com/sdk/docs/authorizing#authorizing_with_a_user_account).

On your working directory, define your Objectives and Indicator selectors with:

```console
reliably slo init
```

<CopyToClipboard />

When you're done, the CLI will confirm your manifest has been successfully created in your working directory.

```reliably
<span class="token green">✓</span> Your manifests has been saved to ./reliably.yaml
````

You must then sync your manifest with Reliably's API:

```console
reliably slo sync
```

<CopyToClipboard />

</Tab>
<Tab name="Datadog">

### Datadog

To get started you will need:

1. A Datadog account
2. Data collected and available
3. An environment configured with the variables: `DD_SITE`, `DD_API_KEY`, `DD_APP_KEY`. More information can be found in Datadog's [API and Application Keys](https://docs.datadoghq.com/account_management/api-app-keys/) section.
4. Two Datadog queries for each Objective/Indicator pair: a numerator query (representing good events in your system) and a denominator query (representing total events). This will allow the `reliably` CLI to calculate how reliably your service is performing based on these metrics.

On your working directory, define your Objectives and Indicator selectors with:

```console
reliably slo init
```

<CopyToClipboard />

When you're done, the CLI will confirm your manifest has been successfully created in your working directory.

```reliably
<span class="token green">✓</span> Your manifests has been saved to ./reliably.yaml
````

You must then sync your manifest with Reliably's API:

```console
reliably slo sync
```

<CopyToClipboard />

</Tab>
<Tab name="Prometheus">

### Prometheus

To get started you will need:

1. The URL to a Prometheus instance that allows unauthenticated access to its API
2. One Prometheus query that returns a ratio of good events against all events
   seen for a particular metric. Make sure this query returns a
   [scalar](https://prometheus.io/docs/prometheus/latest/querying/api/#scalars)
   or a [instant vector](https://prometheus.io/docs/prometheus/latest/querying/api/#instant-vectors)
   only.

On your working directory, define your Objectives and Indicator selectors with:

```console
reliably slo init
```

<CopyToClipboard />

When you're done, the CLI will confirm your manifest has been successfully created in your working directory.

```reliably
<span class="token green">✓</span> Your manifests has been saved to ./reliably.yaml
````

You must then sync your manifest with Reliably's API:

```console
reliably slo sync
```

<CopyToClipboard />

</Tab>
<Tab name="Custom Objectives">

### Custom Objectives

If the resources you are targeting are not available as an integration, you may define your manifest manually. This can also be useful for seasoned users that know the exact values they would like to define in their manifest.

The [Sending Custom Indicators](/docs/guides/slo/sending-custom-indicators/) section will guide you through the process of creating Objectives and Indicators manually.

:::warning Warning
If defining custom Objectives, you will not be able to leverage `reliably slo agent` if the data provider is not supported. However, this will give you the flexibility to push Indicators from any source.
:::

</Tab>
</Tabs>

## Push Indicators

Once you have defined your Objectives and Indicator selectors, it's time to configure a way to push Indicators to Reliably's API. When these Indicators are received, they will be matched with any Objective that has the appropriate selector for that Indicator. This will then record an Objective Result.

There are two primary ways to push Indicators. You may deploy or locally run the CLI in `agent` mode, or push custom Indicators manually, with an API client such as `curl`.

For a brief introduction on how this works, it is recommended to run in agent mode locally which will allow you to view results immediately.

<Tabs>
<Tab name="Agent" selected="true">

### Agent

When running in agent mode, the CLI will periodically request data from your data provider, calculate Indicators, and push them to Reliably's API. For production use, you may deploy the agent so it runs continuously.

If you ran `reliably slo init` in the previous section, you should use the same credentials in your environment in order for the command to access the data provider.

Run the CLI in agent mode with:

```console
reliably slo agent
```

<CopyToClipboard />

Additional options for the agent can be found in the [Reference - agent](/docs/reference/cli/reliably-slo-agent/) section.

</Tab>
<Tab name="Custom Indicators - curl">

### Custom Indicators - curl

If you have chosen to push custom Indicators, you may do so with a tool such as `curl`.

<!-- Choosing not to go in-depth here for the time being. -->

The [Sending Custom Indicators](/docs/guides/slo/sending-custom-indicators/) section will guide you through this the process.

</Tab>
</Tabs>

## View your report

Finally, once you've pushed Indicators and generated Objective Results, you may see your results by running:

```console
reliably slo report
```

<CopyToClipboard />

At this stage you should be able to view the results table of the Objectives you defined combined with the Indicators you have pushed.

An example of the default view:

```reliably
<span class="token dollar"></span>reliably slo report
                                          <span class="token purple bold">Current Objective</span>   <span class="token purple bold">/ Time Window</span>  <span class="token purple bold">Type</span>             <span class="token purple bold">Trend</span>
  Service #1: http-api
  <span class="token emoji">✅</span> Availability over 1 hour           <span class="token green bold">100.00%</span>  99%        /  1h0m0s      Availability     <span class="token green">✓ ✓ ✓ ✓</span>
  <span class="token emoji">❌</span> Request latency under 1s           <span class="token red bold">98.59%</span>   99.9%      /  1d          Latency          <span class="token green">✓ ✓ ✓ ✓</span><span class="token red"> ✕</span>

  Service #2: products-api
  <span class="token emoji">✅</span> Availability over 1 day            <span class="token green bold">100.00%</span>  99%        /  1d          Availability      <span class="token green">✓ ✓ ✓ ✓ ✓</span>
  <span class="token emoji">✅</span> Request latency under 200ms        <span class="token green bold">100.00%</span>  99.5%      /  1d          Latency           <span class="token green">✓ ✓ ✓ ✓ ✓</span>
```

Additional information about the `report` command can be found in [Generate SLO Reports](/docs/guides/slo/slo-reports/).

## What's next?

- Deep-dive on [Objectives, Indicators, Results and Behaviour](/docs/guides/how-it-works/objectives-indicators-results-and-behaviour/)
<!-- - Deploy an agent -->
- [Custom Indicators](/docs/guides/slo/sending-custom-indicators/)
<!-- - Add behaviour like slack alerts -->