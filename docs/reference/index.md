---
title: Reference
excerpt: A detailed guide to all the aspects of Reliably (CLI, entity server...)
categories: ["reference"]
status: published
type: overview
---
import PageIntroduction from '~/components/PageIntroduction.vue'
import SectionList from '~/components/SectionList.vue'

import data from '~/data/reference-index-data.json'

# Reference

<PageIntroduction>
  The reference part of Reliably Documentation is a detailed guide to all the aspects of Reliably.
</PageIntroduction>

<SectionList
    title="Entities"
    categoryName="entities"
    description="Complete reference guide for the Reliably Entity Server"
    link="/reference/entities/"
    :list="data.entities.links"
/>

<SectionList
    title="CLI"
    categoryName="cli"
    description="Complete reference guide for the Reliably CLI"
    link="/reference/cli/"
    :list="data.cli.links"
/>
