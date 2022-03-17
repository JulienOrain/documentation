---
title: reliably graph agent
excerpt: Documentation for the reliably graph agent command in the Reliably CLI
categories: ["reference", "cli"]
status: published
type: doc
---
## reliably graph agent

runs in agent mode sending SLIs to Reliably

### Synopsis

Runs the CLI in SLO agent mode. This mode utilises data defined
on reliably.com or a specified slo manifest to retrieve metrics and generate indicators.

The indicators are sent to reliably.

```
reliably graph agent [flags]
```

### Examples

```
$ reliably slo agent --interval 600
$ reliably slo agent --use-reliably=false -m reliably.yaml -i 300
```

### Options

```
  -h, --help              help for agent
  -i, --interval int      interval indicators are pushed at in seconds (default 300)
  -m, --manifest string   the location of the manifest file (default "reliably.yaml")
  -R, --report-view       shows a view of the report while pushing indicators
  -l, --selector string   objectives selector based on labels - only used when --report-view/-R flag is used
  -r, --use-reliably      retrieve objectives from reliably.com rather than a local manfiest file (default true)
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably graph](/docs/reference/cli/reliably-graph/)	 - Manage entities within your reliably graph

