---
title: CLI Reference
excerpt: The complete Reliably CLI reference.
categories: ["reference", "cli"]
status: published
type: overview
---
import PageIntroduction from '~/components/PageIntroduction.vue'
import MarkdownTwoColumns from '~/components/MarkdownTwoColumns.vue'
import BigLink from '~/components/BigLink.vue';
import OtherArticles from '~/components/OtherArticles.vue'

import IconLogin from '~/assets/images/icons/log-in.svg';
import IconFilter from '~/assets/images/icons/filter.svg';
import IconSearch from '~/assets/images/icons/search.svg';
import IconActivity from '~/assets/images/icons/activity.svg';

import data from '~/data/cli-index-data.json'

# CLI Reference

<PageIntroduction>

The Reliably CLI is the reliability toolbox for developers from the command
line. The articles in this section are the reference pages for the CLI,
containing the details of each CLI command.

Installation for the CLI is covered in the [Getting Started][cli-install]
section.

</PageIntroduction>

[cli-install]: /docs/getting-started/install/

## Main articles

<MarkdownTwoColumns>
  <BigLink to="/reference/cli/reliably-auth/" :external="false" :dark="true">
    <template v-slot:header>
      reliably auth
    </template>
    <template v-slot:icon>
      <IconLogin />
    </template>
    <p>Log in, log out, and verify your authentication with Reliably.</p>
  </BigLink>
  <BigLink to="/reference/cli/reliably-workflow/" :external="false" :dark="true">
    <template v-slot:header>
      reliably workflow
    </template>
    <template v-slot:icon>
      <IconFilter />
    </template>
    <p>Setup Reliably in your CI/CD workflow.</p>
  </BigLink>
  <BigLink to="/reference/cli/reliably-scan/" :external="false" :dark="true">
    <template v-slot:header>
      reliably scan
    </template>
    <template v-slot:icon>
      <IconSearch />
    </template>
    <p>Scan your Kubernetes manifests or cluster for Reliably Suggestions.</p>
  </BigLink>
  <BigLink to="/reference/cli/reliably-slo/" :external="false" :dark="true">
    <template v-slot:header>
      reliably slo
    </template>
    <template v-slot:icon>
      <IconActivity />
    </template>
    <p>The Reliably Service Level Objectives command</p>
  </BigLink>
</MarkdownTwoColumns>

## Other articles

<OtherArticles :links="data.links" />
