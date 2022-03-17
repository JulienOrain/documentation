---
title: reliably populate kube
excerpt: Documentation for the reliably populate kube command in the Reliably CLI
categories: ["reference", "cli"]
status: published
type: doc
---
## reliably populate kube

create Reliably Entities from Kubernetes Infrastructure

### Synopsis


Populate your Reliably Network with Entities based
on your Kubernetes resources.

Reliably CLI will automatically detect your kubernetes
configuration file and use it to query your cluster.

You are able to query specific namespaces and contexts
by using the flags -n/--namespace & -c/--kubecontext respectively. You can also 
specify a path to your Kube Config file using -k/--kubeconfig

NOTE: Prometheus is required to support the SLOs created
by the feature, if no Prometheus endpoint is provided, 
only the descriptive entities will be created and the objectives
will be skipped.

```
reliably populate kube [flags]
```

### Examples

```

specify the kubernetes config file and context to populate your kubernetes network from
$ reliably entity populate kube -k path/to/kube/config.yml -c <your context here>

specify the prometheus endpoint for retrieving metrics
$ reliably entity populate kube -p http://localhost:9090

populate your kubernetes network with resources from the specified namespace
$ reliably entity populate kube -n <your namespace>

populate your kubernetes network with deployment and pod entities
$ reliably entity populate kube -r deployments -r pods
```

### Options

```
  -h, --help                        help for kube
  -k, --kubeconfig string           path to kubernetes config file
  -c, --kubecontext string          Specifies the Kubernetes context to evaluate when scanning live cluster
  -n, --namespace string            specify kubernetes namespace (default "default")
  -p, --prometheus-url string       prometheus endpoint used to retrieve metrics
  -r, --resource-type stringArray   selected kubernetes resource types: supports (deployments, services, pods)
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably populate](/docs/reference/cli/reliably-populate/)	 - populate your reliably graph

