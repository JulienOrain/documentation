---
title: reliably agent
excerpt: Documentation for the reliably agent command in the Reliably CLI
layout: ~/layouts/DocsLayout.astro
---
## reliably agent

runs in agent mode sending SLIs to Reliably

### Synopsis

Runs the CLI in SLO agent mode. This mode identifies and creates
SLIs (service level indicators) for all SLO/Objectives created
by the reliaby populate [provider] command.

Note that each reliably provider type will require the relevant
access permissions

```
reliably agent [flags]
```

### Examples

```
run SLI agent with a fetch interval of 600 seconds
$ reliably agent --interval 600

run a single iteration of the SLI agent
$ reliably agent
```

### Options

```
  -h, --help           help for agent
  -i, --interval int   interval indicators are pushed at in seconds
                       If interval is 0 or not given the agent will
                       run a single iteration
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably](/docs/reference/cli/reliably/)	 - Reliably CLI

