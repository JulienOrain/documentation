---
title: reliably slo related
excerpt: Documentation for the reliably slo related command in the Reliably CLI
categories: ["reference", "cli"]
status: published
type: doc
---
## reliably slo related

fetches a node graph of relationships based on manifest objectives

### Synopsis

By defining the metadata.relatedTo keyword, arbitrary relationships
between 2 or more entities can be described. 

The [related] command uses the defined relationships to generate a 
Node Graph visualisation of the relationships defined. Some relationships
are defined automatically, for eg. Indicator --> Objectives or 
Objective Results --> Objectives.

By default the [related] command will return a graph of ALL entities within
the organisation. A more specific view can be obtained by passing a manifest using
--manifest/-m, this will return a graph of entites relating to those in the manifest
provided. --filters/-f flags can also be used to filter nodes.

Passing the --raw/-r flag will return the raw JSON data used to draw
the graph. 

NOTE: the raw JSON data can also be retrieved by going to /data
when running the visualisation in a browser

```
reliably slo related [flags]
```

### Examples

```
open visualisation on a random port between 60000-61000 for all entities within the organisation
$ reliably slo related

open visualisation app on port 8085 showing all entity relationships originating from those defined in the given manifest
$ reliably slo related -m reliably.yaml --port 8085

return raw JSON blob of visualisation data for all entities
$ reliably slo related --raw

open visualisation app on random port, only showing nodes with labels matching the given filters
$ reliably slo related --filter 'key=value' --filter 'key=value'
```

### Options

```
  -f, --filters stringArray   <key=value> labels to filter relationship graph nodes
  -h, --help                  help for related
  -m, --manifest string       the location of the manifest file
  -p, --port string           the port to serve the graph visualisation on. A random port [60000-61000] is used if no port is profided
  -r, --raw                   prints raw json graph data
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably slo](/docs/reference/cli/reliably-slo/)	 - service level objective commands

