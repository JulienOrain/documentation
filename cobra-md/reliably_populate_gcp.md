---
title: reliably populate gcp
excerpt: Documentation for the reliably populate gcp command in the Reliably CLI
categories: ["reference", "cli"]
status: published
type: doc
---
## reliably populate gcp

create Reliably Entities from Google Cloud Platform Infrastructure

### Synopsis


Populate your Reliably Network with Entities based 
on your Google Cloud Platform (GCP) resources.

Only supported resources can be added by this
command. (cloudrun, cloudfunction)...

You must have access to Google Cloud Platform and your
credentials configured for SDK use.
See: https://cloud.google.com/docs/authentication/getting-started


```
reliably populate gcp [flags]
```

### Examples

```

populate your network with resources from GCP, 
you will be prompted for Project ID and Resource types
$ reliably graph populate gcp

sepcify Porject ID to populate your network with resources from GCP
$ reliably graph populate gcp --project abc-123

populate your network with resources from GCP using select mode
you will be prompted to select which resources to add
$ reliably graph populate gcp --select

```

### Options

```
  -h, --help                        help for gcp
  -p, --project string              Google Cloud project id
  -r, --resource-type stringArray   selected Google Cloud resource types: supports (cloudrun, cloudfunction)
      --select                      select which resources to add from list of available items
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably populate](/docs/reference/cli/reliably-populate/)	 - populate your reliably environment

