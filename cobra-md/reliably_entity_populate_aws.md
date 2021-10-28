---
title: reliably entity populate aws
excerpt: Documentation for the reliably entity populate aws command in the Reliably CLI
categories: ["reference", "cli"]
status: published
type: doc
---
## reliably entity populate aws

creates Reliably Entities from AWS Cloudformation Stacks

### Synopsis


Populates your Reliably Network with Entities
based on the Resources and Relationships found
within the selected AWS CloudFormation Stacks

Stack names must be given in the format: --stacks stackname1,stackname2,stackname3...

If no --stacks are provided, you will be prompted
to select from a list of Stacks found in your AWS account

```
reliably entity populate aws [flags]
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

* [reliably entity populate](/docs/reference/cli/reliably-entity-populate/)	 - 

