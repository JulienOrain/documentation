---
title: Getting started
excerpt: Set up and start using the Reliably CLI.
categories: ["getting-started"]
status: published
type: overview
---
import PageIntroduction from '~/components/PageIntroduction.vue'
import MarkdownTwoColumns from '~/components/MarkdownTwoColumns.vue'
import OtherArticles from '~/components/OtherArticles.vue'
import BigLink from '~/components/BigLink.vue';

import IconInstall from '~/assets/images/icons/download.svg';
import IconUpgrade from '~/assets/images/icons/arrow-up-right.svg';
import IconLogin from '~/assets/images/icons/log-in.svg';
import IconPlugin from '~/assets/images/icons/box.svg';

import data from '~/data/getting-started-index-data.json'

# Get started with Reliably

<PageIntroduction>
  The easiest and quickest way of getting started with Reliably is to run the Reliably CLI on your machine with your local source code files. Here's a link to the  <a href="/docs/getting-started/install/#quick-install-guide">quick install guide</a>.
</PageIntroduction>

## Main articles

<MarkdownTwoColumns>
  <BigLink to="/getting-started/install/" :external="false" :dark="true">
    <template v-slot:header>
      Install Reliably
    </template>
    <template v-slot:icon>
      <IconInstall />
    </template>
    <p>Install the Reliably CLI and make your first Kubernetes manifest more reliable in minutes.</p>
  </BigLink>
  <BigLink to="/getting-started/login/" :external="false" :dark="true">
    <template v-slot:header>
      Login to Reliably
    </template>
    <template v-slot:icon>
      <IconLogin />
    </template>
    <p>Authenticate the Reliably CLI with Reliably.com</p>
  </BigLink>
  <BigLink to="/getting-started/slos/" :external="false" :dark="true">
    <template v-slot:header>
      Define and Observe your Reliability
    </template>
    <template v-slot:icon>
      <IconLogin />
    </template>
    <p>Define and observe your reliability by implementing Service Level Objectives</p>
  </BigLink>
  <BigLink to="/getting-started/scanning-k8s/" :external="false" :dark="true">
    <template v-slot:header>
      Applying 'best practice' to Kubernetes
    </template>
    <template v-slot:icon>
      <IconLogin />
    </template>
    <p>Scan a Kubernetes cluster for adherence to best practice</p>
  </BigLink>
</MarkdownTwoColumns>

