---
title: reliably graph populate
excerpt: Documentation for the reliably graph populate command in the Reliably CLI
categories: ["reference", "cli"]
status: published
type: doc
---
## reliably graph populate

populate your reliably graph

### Synopsis

The reliably slo populate command fasicilates populating your Relaibly graph
with pre-supported entities/objectives from various platforms. 

All objectives created by the populate command are directly supported
by the reliably slo agent command for pushing indicators.


### Options

```
  -h, --help   help for populate
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably graph](/docs/reference/cli/reliably-graph/)	 - Manage entities within your reliably graph
* [reliably graph populate aws](/docs/reference/cli/reliably-graph-populate-aws/)	 - creates Reliably Entities from AWS Cloudformation Stacks
* [reliably graph populate gcp](/docs/reference/cli/reliably-graph-populate-gcp/)	 - create Reliably Entities from Google Cloud Platform Infrastructure
* [reliably graph populate github](/docs/reference/cli/reliably-graph-populate-github/)	 - create Reliably Entities from Github Repositories
* [reliably graph populate kube](/docs/reference/cli/reliably-graph-populate-kube/)	 - create Reliably Entities from Kubernetes Infrastructure

