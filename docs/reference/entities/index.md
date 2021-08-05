---
title: Common Properties
excerpt: The definition of properties common to all entities
categories: ["reference", "entities"]
status: published
type: overview
---
import PageIntroduction from '~/components/PageIntroduction.vue'
import MarkdownTwoColumns from '~/components/MarkdownTwoColumns.vue'
import BigLink from '~/components/BigLink.vue';
import OtherArticles from '~/components/OtherArticles.vue'

import IconCommon from '~/assets/images/icons/refresh-cw.svg';
import IconActivity from '~/assets/images/icons/activity.svg';

import data from '~/data/entities-index-data.json'

# Entities Reference

<PageIntroduction>

The Reliably Entity Server holds the state of service levels for an organisation remotely, for consumption by other tools.

</PageIntroduction>

## Main articles

<MarkdownTwoColumns>
  <BigLink to="/reference/entities/common-properties/" :external="false" :dark="true">
    <template v-slot:header>
      Common Properties
    </template>
    <template v-slot:icon>
      <IconCommon />
    </template>
    <p>All Reliably manifests share certain common properties. They are described here.</p>
  </BigLink>
  <BigLink to="/reference/entities/indicator/" :external="false" :dark="true">
    <template v-slot:header>
      Indicator
    </template>
    <template v-slot:icon>
      <IconActivity />
    </template>
    <p>An Indicator declaratively defines a single Service Level Indicator</p>
  </BigLink>
</MarkdownTwoColumns>

## Other articles

<OtherArticles :links="data.links" />
