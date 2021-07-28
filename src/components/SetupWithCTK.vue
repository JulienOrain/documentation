<template>
<span class="setup">
    <h2 id="before-you-begin"><a href="#before-you-begin" aria-hidden="true">#</a>Before you begin</h2>
    <h3 id="install"><a href="#install" aria-hidden="true">#</a>Install Reliably</h3>
    <p>If you haven't already, you will first need to <a href="/docs/getting-started/install/#quick-install-guide">install Reliably's CLI</a>.</p>
    <h3 id="login"><a href="#login" aria-hidden="true">#</a>Login</h3>
    <p>Once you install the CLI, make sure you are logged in with:</p>
    <pre class="language-console"><code class="language-console">reliably auth login</code></pre>
    <CopyToClipboard />
    <p> Additional information can be found in the <a href="/docs/getting-started/login/#login">Login</a> section.</p>
    <h3 id="install-ctk"><a href="#install-ctk" aria-hidden="true">#</a>Install Chaos Toolkit</h3>
    <p>To use Chaos Toolkit, you'll need <a href="https://www.python.org/downloads/">Python 3.6+</a> installed, you can then get Chaos Toolkit and its Reliably plugin with:</p>
    <pre class="language-console"><code class="language-console">python -m venv .venv && source .venv/bin/activate</code></pre>
    <CopyToClipboard />
    <pre class="language-console"><code class="language-console">pip install -U chaostoolkit chaostoolkit-reliably</code></pre>
    <CopyToClipboard />
    <p>You can confirm which version of Chaos Toolkit you've just installed with:</p>
    <pre class="language-console"><code class="language-console">chaos --version</code></pre>
    <CopyToClipboard />
  </span>
</template>

<script>

import CopyToClipboard from '~/components/MarkdownCopyToClipboard.vue'

export default {
    components: {
        CopyToClipboard
    }
}
</script>

<style lang="scss" scoped>
.setup {
    h2, h3, p {
        margin-bottom: 0;
    }
}
</style>
