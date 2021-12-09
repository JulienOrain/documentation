---
title: reliably entity create operation
excerpt: Documentation for the reliably entity create operation command in the Reliably CLI
categories: ["reference", "cli"]
status: published
type: doc
---
## reliably entity create operation

Creates a new operation entity

### Synopsis

Creates a new operation entity. An operation is anything of note within your system, that has an outcome.

A few examples of operations:

* a build completed successfully, or failed.
* a deployment completed successfully, or failed.
* documentation was created.

```
reliably entity create operation [flags]
```

### Examples

```
reliably entity create operation --service 'my awesome service' --type build --outcome success
```

### Options

```
  -h, --help             help for operation
      --outcome string   the outcome of the operation
      --service string   the service that this operation is being performed on
      --type string      the type of operation being performed
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably entity create](/docs/reference/cli/reliably-entity-create/)	 - entry point to create entities

