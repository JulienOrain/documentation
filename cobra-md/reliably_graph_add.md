---
title: reliably graph add
excerpt: Documentation for the reliably graph add command in the Reliably CLI
categories: ["reference", "cli"]
status: published
type: doc
---
## reliably graph add

add the objectives from your manifest with Reliably

### Synopsis

The reliably slo add command reads from a given reliably.yaml manifest
and populates your Reliably network with any valid Entities
detected.

Note that entities with the same metadata as existing entities
will be overwritten.


```
reliably graph add [flags]
```

### Examples

```
add entities from a given manifest yaml file
$ reliably slo add -m reliably.yaml

```

### Options

```
  -h, --help              help for add
  -m, --manifest string   path of the manifest to sync up (default "reliably.yaml")
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably graph](/docs/reference/cli/reliably-graph/)	 - Manage entities within your reliably graph

