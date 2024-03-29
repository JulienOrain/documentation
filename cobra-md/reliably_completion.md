---
title: reliably completion
excerpt: Documentation for the reliably completion command in the Reliably CLI
layout: ~/layouts/DocsLayout.astro
---
## reliably completion

Generate shell completion scripts

### Synopsis

Generate shell completion scripts for Reliably CLI commands.

The output of this command will be computer code and is meant to be saved to a
file or immediately evaluated by an interactive shell.

For example, for bash you could add this to your '~/.bash_profile':
  eval "$(reliably completion -s bash)"

```
reliably completion -s <shell>
```

### Options

```
  -h, --help           help for completion
  -s, --shell string   Shell type: {bash|zsh|fish|powershell}
```

### Options inherited from parent commands

```
      --no-color       Disable color output
  -v, --verbose        verbose output
  -V, --very-verbose   very verbose output
```

### SEE ALSO

* [reliably](/docs/reference/cli/reliably/)	 - Reliably CLI

