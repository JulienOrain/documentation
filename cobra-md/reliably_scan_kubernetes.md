---
title: reliably scan kubernetes
excerpt: Documentation for the reliably scan kubernetes command in the Reliably CLI
categories: ["reference", "cli"]
status: published
type: doc
---
## reliably scan kubernetes

Check for Reliably Suggestions for your Kubernetes resources

### Synopsis

Check your Kubernetes manifests for Reliably Suggestions.

Manifest(s) can be provided in several ways:
- read from standard input, with dash '-' as argument
- path to a single manifest file
- path to a folder that will be scanned recursively for manifests files

By default, the scan command, run without arguments, is scanning
manifests file from the current working directory.

Reliably can also scan for your live kubernetes cluster.

```
reliably scan kubernetes [path] [flags]
```

### Examples

```
# Scan a single file:
$ reliably scan kubernetes manifest.yaml

# Scan a folder:
$ reliably scan
$ reliably scan .
$ reliably scan ./manifests

# Scan with reading manifest from stdin:
$ cat manifest.yaml | reliably scan -

# Scan with custom format & output to local file
$ reliably scan --format json --output report.json

# Ignore specific rules
$ reliably scan kubernetes --ignore-rules K8S-POD-0002,K8S-DPL-0004

# Ignore rules defined in a .json file
$ reliably scan kubernetes --ignore-rules exceptions.json

# Scan a live Kubernetes cluster
$ reliably scan --live
$ reliably scan --live [--namespace n] [--kubecontext c] [--kubeconfig c]
```

### Options

```
  -f, --format string         Specify the output format: [text json yaml sarif codeclimate extended table]
  -h, --help                  help for kubernetes
  -i, --ignore-rules string   Ignore rules defined in standard input or from a provided .json file
  -k, --kubeconfig string     Specifies the path and file to use for kubeconfig for live scan (default "/home/runner/.kube/config")
  -c, --kubecontext string    Specifies the Kubernetes context to evaluate when scanning live cluster
  -l, --level string          Display suggestions only for level and higher
      --live                  Look for weaknesses in a live Kubernetes cluster
  -n, --namespace string      The namespace to use when using a live cluster
  -o, --output string         Write results to a file instead of standard output
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably scan](/docs/reference/cli/reliably-scan/)	 - Check for Reliably Suggestions

