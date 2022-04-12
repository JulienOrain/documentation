---
title: reliably populate aws
excerpt: Documentation for the reliably populate aws command in the Reliably CLI
layout: ~/layouts/DocsLayout.astro
---
## reliably populate aws

creates Reliably Entities from AWS Cloudformation Stacks

### Synopsis


Populates your Reliably Network with Entities
based on supported AWS Resources and Relationships

This command will scan all supported resources and created objectives.
The --select or --resource flags can be used you to select which resource types to scan.

Note - You must have AWS Credentials configured to used this
command. See https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html

```
reliably populate aws [flags]
```

### Examples

```

populate your network with AWS Lambda based Objectives
$ reliably populate aws --resource lambda

run the populate command in interactive select mode
$ reliably populate aws --select

specify AWS Profile while running populate command
$ AWS_DEFAULT_PROFILE=<named-profile> reliably populate aws

specify AWS Region while running populate command
$ AWS_DEFAULT_REGION=<region-name> reliably populate aws
```

### Options

```
  -h, --help                   help for aws
  -r, --resource stringArray   select AWS resource types:
                               
                               	- lambda
                               	- cloudformation
                               	- apigateway
                               	- elasticloadbalancer
                               
      --select                 select which resource types to add from list of supported types
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably populate](/docs/reference/cli/reliably_populate/)	 - populate your reliably environment

