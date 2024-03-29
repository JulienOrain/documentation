---
title: reliably auth login
excerpt: Documentation for the reliably auth login command in the Reliably CLI
layout: ~/layouts/DocsLayout.astro
---
## reliably auth login

Authenticate with Reliably

### Synopsis

Authenticate with Reliably.

The default authentication mode is interactive and asking for a token.

Alternatively, pass in a token on standard input by using '--with-token'.

```
reliably auth login [flags]
```

### Examples

```
# start interactive authentication setup
$ reliably auth login

# authenticate by reading the token from a file
$ reliably auth login --with-token < my-access-token.txt
```

### Options

```
  -h, --help              help for login
      --hostname string   The hostname of Reliably to authenticate with
      --provider string   The provider for Reliably to authenticate with
      --with-token        Read token from standard input
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably auth](/docs/reference/cli/reliably_auth/)	 - Login, logout, and verify your authentication

