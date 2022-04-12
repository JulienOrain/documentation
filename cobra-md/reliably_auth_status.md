---
title: reliably auth status
excerpt: Documentation for the reliably auth status command in the Reliably CLI
layout: ~/layouts/DocsLayout.astro
---
## reliably auth status

View authentication status

### Synopsis

Verifies and displays information about your authentication to Reliably.

This command will test your authentication token to ensure
it's still valid and report on any issue.

```
reliably auth status [flags]
```

### Options

```
  -h, --help              help for status
      --hostname string   Check a specific hostname's auth status
  -t, --show-token        Display the auth token
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably auth](/docs/reference/cli/reliably_auth/)	 - Login, logout, and verify your authentication

