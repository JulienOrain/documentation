---
title: reliably populate github
excerpt: Documentation for the reliably populate github command in the Reliably CLI
layout: ~/layouts/DocsLayout.astro
---
## reliably populate github

create Reliably Entities from Github Repositories

### Synopsis


Populate your Reliably Network with Entities
based on the Github repositories within your
organisation.

Repository names can be passed using the -r/--repo flags
in the format 'github.com/:org/:name'. If no repo
names are given, then you will be prompted with a list
of repositories available to you based on your Github
access token.

Note: This feature requires privileged access to Github.
You will be prompted to login if no Github Access token
is provided.

The ENV variable GITHUB_TOKEN can be used to pass an oath
token from the environment.


```
reliably populate github [flags]
```

### Examples

```

populate your network with github repositories
- you will be prompted to login if no github token is detected
- a list of available repos will be displayed
$ reliably populate github

populate your network with the github repositories you specify.
you must have have access to the repositories specificed
$ reliably populate github  --repo github.com/repo/two --repo github.com/repo/one

populate your network with github repositories using the GH CLI token if it exists
$ reliably populate github --gh-cli-token

populate your network with github repositories using a given token
$ reliably populate github --with-token < my-access-token.txt

trigger interactive authentication and populate your network with github repositories
$ reliably populate github --login

pass a token using an environment variable
$ GITHUB_TOKEN=<your_token_here> reliably populate github

```

### Options

```
      --gh-cli-token       use github CLI token, if present
  -h, --help               help for github
      --login              login to github via browser
  -r, --repo stringArray   selected repositories, must be in the form 'github.com/:org/:name'
      --with-token         read github token from standard input
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably populate](/docs/reference/cli/reliably_populate/)	 - populate your reliably environment

