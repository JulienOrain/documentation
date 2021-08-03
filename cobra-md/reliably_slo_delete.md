---
title: reliably slo delete
excerpt: Documentation for the doc/cobra-md/reliably_slo_delete.md command in the Reliably CLI
categories: ["reference", "cli"]
status: published
type: doc
---
## reliably slo delete

deletes Objectives based on given manifest/selectors

### Synopsis


Deletes Objectives based on the given manifest or selector.
Note that if both --manifest and --selector are specified,
the selectors will be prioritized

selectors must be given in the format: --selector 'key=value'

```
reliably slo delete [flags]
```

### Examples

```
delete all entities within an manifest
$ reliably slo delete -m reliably.yaml

delete all enitites that match any of the given selectors, equivalent: (OR statement)
$ reliably slo delete --selector='key=value' --selector='key=value'

delete all entities that match ALL the key=value pairs within the selector, equivalent: (AND statement)
$ reliably slo delete --selector='key=value, key=value, key=value'
```

### Options

```
  -h, --help                   help for delete
  -m, --manifest string        the location of the manifest file (default "reliably.yaml")
  -l, --selector stringArray   key/value pair(s) matching objective labels to be deleted
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably slo](/docs/reference/cli/reliably-slo/)	 - service level objective commands
