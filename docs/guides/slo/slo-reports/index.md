---
title: Generate SLO Reports
excerpt: Use the Reliably CLI to generate Service Level Objective reports.
categories: ["guides", "slo"]
status: published
type: doc
---
import AsciiPlayer from '~/components/AsciiPlayer.vue'
import CopyToClipboard from '~/components/MarkdownCopyToClipboard.vue'

# Generate SLO Reports

Now that you have defined objectives and generated indicators, you can use the Reliably CLI to view your SLO report. This is done with the `reliably slo report` command.

## Usage

```console
reliably slo report
```

<CopyToClipboard />

<AsciiPlayer id="409053" />

The `reliably slo report` command will by default provide results for each objective in your organization. There are two ways to filter the report.

### Selector Filter

- You may filter by using the `-l, --selector` flag with a selector such as `service=example_api,category=latency`.

```console
reliably slo report -l service=example_api,category=latency
```

<CopyToClipboard />

### Manifest Filter

- Additional filtering can be done with a manifest file and the flag `-m`. This filters your report to only view the objectives defined in your manifest.

```console
reliably slo report -m reliably.yaml
```

<CopyToClipboard />

## Output Format

You can select between output formats with the `--format` or `-f` flag.

### Table Output

Table output is the default format for SLO reports.

```console
reliably slo report --format table
```

<CopyToClipboard />

```reliably
<span class="token dollar"></span>reliably slo report --format table
                                          <span class="token purple bold">Current Objective</span>   <span class="token purple bold">/ Time Window</span>  <span class="token purple bold">Type</span>             <span class="token purple bold">Trend</span>
  Service #1: http-api
  <span class="token emoji">✅</span> 99% availability over 1 hour         <span class="token green bold">100.00%</span>  99%        /  1h0m0s      Availability     <span class="token green">✓ ✓ ✓ ✓</span>
  <span class="token emoji">✅</span> 99.5% availability over 1 day        <span class="token green bold">100.00%</span>  99.5%      /  1d          Availability     <span class="token green">✓ ✓ ✓ ✓ ✓</span>
  <span class="token emoji">❌</span> 99% of requests under 300ms          <span class="token red bold">77.46%</span>   99%        /  1d          Latency          <span class="token green">✓</span> <span class="token red">✕</span> <span class="token green">✓ ✓</span><span class="token red"> ✕</span>
  <span class="token emoji">❌</span> 99.9% of requests under 1s           <span class="token red bold">98.59%</span>   99.9%      /  1d          Latency          <span class="token green">✓ ✓ ✓ ✓</span><span class="token red"> ✕</span>

  Service #2: products-api
  <span class="token emoji">✅</span> 99% availability over 1 day          <span class="token green bold">100.00%</span>  99%        /  1d          Availability      <span class="token green">✓ ✓ ✓ ✓ ✓</span>
  <span class="token emoji">✅</span> 99.5% of requests under 200ms        <span class="token green bold">100.00%</span>  99.5%      /  1d          Latency           <span class="token green">✓ ✓ ✓ ✓ ✓</span>
```

### Text Output

The text output will remove the tabs, and use glyphs instead of emojis for
your SLO status, and will not display SLO target and delta.

```console
reliably slo report --format text
```

<CopyToClipboard />

```reliably
<span class="token dollar"></span>reliably slo report --format text
<span class="token yellow">Service #1: http-api</span>
<span class="token green">✓</span> 99% availability over 1 hour: 100.00% [objective: 99% / 1h0m0s, delta: 1.00%, type: Availability]
<span class="token green">✓</span> 99.5% availability over 1 day: 100.00% [objective: 99.5% / 1d, delta: 0.50%, type: Availability]
<span class="token red">✕</span> 99% of requests under 300ms: 77.46% [objective: 99% / 1d, delta: -21.54%, type: Latency]
<span class="token red">✕</span> 99.9% of requests under 1s: 98.59%  [objective: 99.9% / 1d, delta: -1.31%, type: Latency]

<span class="token yellow">Service #2: products-api</span>
<span class="token green">✓</span> 99% availability over 1 day: 100.00% [objective: 99% / 1d , delta: 1.00%, type: Availability]
<span class="token green">✓</span> 99.5% of products API requests under 200ms: 100.00% [objective: 99.5% / 1d, delta: 0.50%, type: Latency]
```

If you want to disable the glyph coloring, you can use the `--no-color` global
flag.

```console
reliably slo report --format text --no-color
```

<CopyToClipboard />

```reliably
<span class="token dollar"></span>reliably slo report --format text --no-color
Service #1: http-api
✓ 99% availability over 1 hour: 100.00% [objective: 99% / 1h0m0s, delta: 1.00%, type: Availability]
✓ 99.5% availability over 1 day: 100.00% [objective: 99.5% / 1d, delta: 0.50%, type: Availability]
✕ 99% of requests under 300ms: 77.46% [objective: 99% / 1d, delta: -21.54%, type: Latency]
✕ 99.9% of requests under 1s: 98.59% [objective: 99.9% / 1d, delta: -1.31%, type: Latency]

Service #2: products-api
✓ 99% availability over 1 day: 100.00% [objective: 99% / 1d, delta: 1.00%, type: Availability]
✓ 99.5% of products API requests under 200ms: 100.00% [objective: 99.5% / 1d, delta: 0.50%, type: Latency]
```

### JSON Output

You can generate a JSON-formatted SLO report for consumption in third-party
tools.

```console
reliably slo report --format json
```

<CopyToClipboard />

### Markdown Output

You can generate a markdown-formatted SLO report.

```console
reliably slo report --format markdown
```

<CopyToClipboard />

:::tip Tip
  You can use a tool like <a href="https://pandoc.org/" target="_blank" rel="noopener noreferer">Pandoc</a> to convert the output generated from Reliably
  into many other formats such as HTML and PDF. To <a href="https://www.geeksforgeeks.org/piping-in-unix-or-linux/" target="_blank" rel="noopener noreferer">pipe</a> the markdown output to pandoc:

  ```console
  reliably slo report --format markdown | pandoc
  ```

  The command above will by default generate HTML output.
:::

### Report Templates

You can use templates to  generate an SLO report. This allows you to build reports using your own format based on templates.

```console
reliably slo report -t /path/to/template.tmpl
```

<CopyToClipboard />

You can combine this with the '-o' option to write the output to a file:

```console
reliably slo report -t /path/to/template.tmpl -o /path/to/report.txt
```

<CopyToClipboard />

The How it Works Guide on [SLO Report Templates] fully explains how to create your own templates for Reliably

[SLO Report Templates]: /docs/guides/other/report-templates/

<!-- This needs to be moved to another area -->
<!-- 
## Provider Authentication

For the CLI to be able to connect to your provider and fetch data, you will need
to be authenticated.

### AWS

Authentication with AWS is made through an `credentials` file in your
`$HOME/.aws` directory.

```
[default]
aws_access_key_id = <your access key>
aws_secret_access_key = <your secret access key>
```

<a href="https://aws.github.io/aws-sdk-go-v2/docs/configuring-sdk/#specifying-credentials/" target="_blank" rel="noopener noreferer">Read more in the AWS SDK docs.</a>

### Google Cloud Platform

You can authenticate be using the `GOOGLE_APPLICATION_CREDENTIALS` environment variable. It is set to the file path of the JSON files that contains your service account key.

```console
export GOOGLE_APPLICATION_CREDENTIALS="/home/user/Downloads/my-key.json"
```
<CopyToClipboard />

<a href="https://cloud.google.com/docs/authentication/getting-started" target="_blank" rel="noopener noreferer">Read more about authentication methods</a> in the Google Cloud documentation.

:::note
To fetch the required data, your service account will need a specific permission: "Monitoring Viewer"
::: -->

## Reference

Read the [Reliably CLI SLO Reports command](/docs/reference/cli/reliably-slo-report/) reference for a complete list of options.
