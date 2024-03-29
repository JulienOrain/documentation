---
title: reliably auth logout
excerpt: Documentation for the reliably auth logout command in the Reliably CLI
layout: ~/layouts/DocsLayout.astro
---
## reliably auth logout

Log out from Reliably

### Synopsis

Remove authentication for Reliably.

This command removes the authentication configuration.

```
reliably auth logout [flags]
```

### Options

```
  -h, --help              help for logout
      --hostname string   The hostname of Reliably to log out of
  -y, --yes               Don't ask for logout confirmation
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably auth](/docs/reference/cli/reliably_auth/)	 - Login, logout, and verify your authentication

