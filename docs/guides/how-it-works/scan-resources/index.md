---
title: How Reliably CLI scans resources
excerpt: What happens when Reliably scans your manifests or clusters for reliability issues?
categories: ["guides", "how-it-works"]
status: published
type: doc
---

import CopyToClipboard from '~/components/MarkdownCopyToClipboard.vue'

# How Reliably CLI works

## Scan Resources

The Reliably CLI will scan your resources to discover any reliability concerns.
It will offer advice on how you can resolve those concerns.

The Reliably CLI will work with files that define your resources, or scan your cluster directly, to work with deployed resources.

For example, to scan for issues in any files in the current working directory
you can run:

```console
reliably scan kubernetes .
```
<CopyToClipboard />

If you want to scan a cluster using your default Kubernetes configuration file,
you can run:

```console
reliably scan kubernetes --live
```
<CopyToClipboard />

The full details of the `reliably scan kubernetes` command are covered in the
[reliably scan kubernetes] section of the reference documentation.

[reliably scan kubernetes]:  /docs/reference/cli/reliably-scan-kubernetes/

### Kubernetes

Currently the Reliably CLI is focussed on supporting the Kubernetes Platform.
Future versions of the CLI will extend to other platforms.

## Fetch rules

The Reliably CLI will Fetch the rules that will be applied to your `scan`
from the Reliably API.

## Display Results

As a result of running a scan, the Reliably CLI will offer advice for any resource issues.

### In your Terminal

If you are running the CLI in your terminal by default, it will display the advice directly in your terminal session:

```reliably
<span class="token dollar"></span>reliably scan kubernetes .
tests/manifests/deployment.yaml:1:1 [<span class="token purple">warning</span>] You should specify a number of replicas
tests/manifests/deployment.yaml:1:1 [<span class="token red">error</span>] Setting a high cpu request may render pod scheduling difficult or starve other pods
tests/manifests/deployment.yaml:1:1 [<span class="token red">error</span>] Not setting a cpu requests means the pod will be allowed to consume the entire available CPU (unless the cluster has set a global limit)
tests/manifests/deployment.yaml:1:1 [<span class="token yellow">info</span>] Image pull policy should usually not be set to 'Always'
tests/manifests/deployment.yaml:1:1 [<span class="token purple">warning</span>] A rollout strategy can reduce the risk of downtime
tests/manifests/deployment.yaml:1:1 [<span class="token red">warning</span>] Without the 'minReadySeconds' property set, pods are considered available from the first time the readiness probe is valid. Settings this value indicates how long it the pod should be ready for before being considered available.
6 suggestions found
```

### In your CI/CD

If you are running the Reliably CLI as part of your adopted CI/CD, then the
output will be displayed within the CI/CD tools. Examples of using different
CI/CD solutions can be seen in the [guides][ci-pipeline].

[ci-pipeline]: /guides/ci-pipeline/

## Results History

Whenever you run a scan with the Reliably CLI, it will store the results from
the scan with the Reliably API.

Only surfaced suggestions and file or resource metadata are stored. Your code
itself never leaves your own premises and is thereby not stored by Reliably.

The API will maintain that history so you can to view progress of your
reliability effort.

## More on that subject

[How the Reliably Genereate SLO Reports](/docs/guides/how-it-works/slo-reports/)

[How the Reliably API works](/docs/guides/how-it-works/api/)

[How the Reliably Rules work](/docs/guides/how-it-works/rules/)

## Not using Reliably yet?

[Getting started with Reliably](/docs/getting-started/)