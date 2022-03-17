---
title: reliably populate aws
excerpt: Documentation for the reliably populate aws command in the Reliably CLI
categories: ["reference", "cli"]
status: published
type: doc
---
## reliably populate aws

creates Reliably Entities from AWS Cloudformation Stacks

### Synopsis


Populates your Reliably Network with Entities
based on the Resources and Relationships found
within the selected AWS CloudFormation Stacks

Stack names must be given in the format: --stacks stackname1,stackname2,stackname3...

If no --stacks are provided, you will be prompted
to select from a list of Stacks found in your AWS account

Note - You must have the AWS CLI (https://aws.amazon.com/cli/) installed
and configured to use this command


```
reliably populate aws [flags]
```

### Examples

```

populate your network with CloudFormation stacks, your available stacks will be displayed
$ reliably entity populate aws

populate your network with specific CloudFormation stacks
$ reliably entity populate aws --stacks stackname1,stackname2

populate your network with CloudFormation stacks from a specific named profile
$ AWS_DEFAULT_PROFILE=<named-profile> reliably entity populate aws

populate your network with CloudFormation stacks from a specific region
$ AWS_DEFAULT_REGION=<region-name> reliably entity populate aws
```

### Options

```
  -h, --help             help for aws
  -s, --stacks strings   comma separated list of AWS CloudFormation Stack Names
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably populate](/docs/reference/cli/reliably-populate/)	 - populate your reliably graph

