---
title: Scanning Kubernetes
excerpt: Scan a kubernetes cluster for adherence to best practice.
categories: ["getting-started"]
status: published
type: doc
---

# Scanning Kubernetes for potential problems

Reliably offers the ability to prevent some issues that can occur in incorrecttly deployed kubernetes applications. The `reliably scan` command is the tool used to scan your infrastructure and deployments for these issues.

<!-- ## Before you get started

* [install the Reliably CLI](../../getting-started/install/index.md)
* [create an organisation](../../getting-started/org-management/index.md) -->

## Whats 'scanning'?

Reliably integrates with [Open Policy Agent](https://github.com/open-policy-agent/opa) to offer the ability to see divergence from best practice in your applications. Adhering to these 'policies' gives a sense of confidence that your application is making use of best practices, and potentially eliminating some issues before they cause trouble - here at Reliably we believe a problem avoided is better than a problem solved!

### Reliably and OPA

So why not just use OPA directly? The answer is a little strange - OPA's most powerful feature is also one of its most complex components. The policies are simultaneously an incredible tool, while also being difficult to write and maintain.

The integration with Reliably means that ReliablyHQ can:
* offer policies that deal with low-hanging fruit, by using our knowledge of running applications 'in the wild' to give you an excellent starting point.
* dynamically update your policies based on what we see happening in your infrastructure.

## How to do it

Run the following command from your command line

```
$ reliably scan kubernetes
```