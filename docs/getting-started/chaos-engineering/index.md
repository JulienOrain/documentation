---
title: Explore the impact on your reliability using Chaos Engineering experiments
excerpt: Create a Chaos Engineering experiment with Chaos Toolkit to impact your reliability
categories: ["getting-started"]
status: published
type: doc
---

import SetupWithCTK from '~/components/SetupWithCTK.vue'
import CopyToClipboard from '~/components/MarkdownCopyToClipboard.vue'

# Explore the impact on your reliability using Chaos Engineering experiments

In this section, you will learn how to explore the impact of your system's reliability when carrying out a Chaos Engineering experiment against it. You'll be using Reliably and [Chaos Toolkit](https://chaostoolkit.org/) to follow this guide; if you've not used Chaos Toolkit before, that's fine!

At a high level, you'll be doing the following:

* Defining an SLO
* Creating a Chaos Engineering experiment
* Running the experiment and viewing its impact on your reliability

<SetupWithCTK />

## Define your Objective

Check out [Define and observe your reliability](/docs/getting-started/slos/) for more information on defining SLOs.

So that you don't need to have any infrastructure already available to follow this guide, you'll be defining a Custom Objective. These allow you to send Custom Indicators to Reliably and appreciate how indicators can be pushed, not just pulled by the Reliably SLO agent.

For this guide, we're providing you with a ready-made Custom Objective; you should copy this Objective into a file called `reliably.yaml`:

```yaml
apiVersion: reliably.com/v1
kind: Objective
metadata:
  labels:
    name: 99.9% of our requests are in the 2xx class
    service: exploring-reliability-guide-service
spec:
  indicatorSelector:
    category: Availability
    indicator_name: exploring-reliability-guide-service-availability-indicator
  objectivePercent: 99.9
  window: 1h
```
<CopyToClipboard />

### Observe your system

Now that you have an SLO defined, you can observe the reliability of your system:

```reliably
<span class="token dollar"></span>reliably slo sync # Uploads your manifest (reliably.yaml) to Reliably
<span class="token dollar"></span>reliably slo report
```
<CopyToClipboard />

```reliably
                                                      <span class="token red bold">Current  Objective  / Time Window     Type     Trend</span>
  Service #1: exploring-reliability-guide-service
```

You'll notice that there's no information. That's because Reliably hasn't had any Indicators that match the `indicatorSelector` yet.

## Create a Chaos Engineering experiment

To keep everything local and mimic a service running, you'll use a Chaos Toolkit Experiment to send `Good` indicators to Reliably.

To make things easier, we've provided you with a ready-made Chaos Toolkit Experiment; you should copy this experiment into a file called `healthy-experiment.json`:

```json
{
    "version": "1.0.0",
    "title": "A Healthy Service",
    "description": "Sends Reliably `Good` Indicators to mimic a healthy service",
    "method": [
        {
            "type": "action",
            "name": "send_good_indicator",
            "provider": {
                "type": "python",
                "module": "reliability_utils",
                "func": "send_good_indicator",
                "arguments": {}
            }
        }
    ]
}
```
<CopyToClipboard />

#### What is this doing?

You've just created a Chaos Toolkit Experiment. The most key section to review is `method`. `method` is where you tell Chaos Toolkit _what_ you're going to do against your system. As you don't have a 'system' in this example, you're using `reliability_utils.send_good_indicator` to pretend you're pinging your service - it's going to report back to Reliably that everything from the last hour is `Good`.

#### `reliability_utils.send_good_indicator`

Copy the following code into a file named `reliability_utils.py`:

```python
from chaoslib.types import Configuration, Secrets
from datetime import datetime
import json

import requests

__all__ = ["send_good_indicator"]

TOKEN = "XXXX"
ORG = "XXXX"


def send_good_indicator(
    configuration: Configuration = None, secrets: Secrets = None
) -> None:
    """
    For a given TOKEN and ORG, send a 100% availability Indicator
    for the selector that matches `category=Availability` and
    `indicator_name=exploring-reliability-guide-service-availability-indicator`
    """
    timenow = datetime.utcnow().isoformat() + 'Z'
    body = {
        "metadata": {
            "labels": {
                "category": "Availability",
                "indicator_name": "exploring-reliability-guide-service-availability-indicator",
            }
        },
        "spec": {"from": timenow, "to": timenow, "percent": 100.0},
    }

    requests.put(
        url=f"https://api.reliably.com/entities/{ORG}/reliably.com/v1/indicator",
        data=json.dumps(body),
        headers={"Authorization": f"Bearer {TOKEN}"},
    )
```
<CopyToClipboard />

Once copied, replace the values of `TOKEN` and `ORG` with the output of the following command:

```reliably
<span class="token dollar"></span>cat ~/.config/reliably/config.yaml
```
<CopyToClipboard />

```reliably
auths:
    reliably.com:
        token: {TOKEN}
        username: your-username
currentOrg:
    name: {ORG}
    id: an-org-id
```

## Getting good reliability

It's time to run your first experiment and see Reliably report your SLO based on the outcome of the experiment.

### Viewing the SLO Report

In a new terminal window, run the following:

```reliably
<span class="token dollar"></span>reliably slo report -w
```
<CopyToClipboard />

```reliably
<span class="token purple">Refreshing SLO report every 3 seconds.</span> Press CTRL+C to quit.
                                                      <span class="token purple bold">Current  Objective  / Time Window     Type     Trend</span>
  Service #1: exploring-reliability-guide-service
```

This will keep the SLO report running so that we can see the `Good` indicator reaching Reliably when we run the experiment.

### Running the healthy experiment

In a different terminal window from the `reliably slo report` one, run the following:

```reliably
<span class="token dollar"></span>PYTHONPATH=. chaos run healthy-experiment.json
```
<CopyToClipboard />

```reliably
<span class="token green">[2021-07-22 09:32:16 INFO]</span> Validating the experiment's syntax
<span class="token green">[2021-07-22 09:32:16 INFO]</span> Experiment looks valid
<span class="token green">[2021-07-22 09:32:16 INFO]</span> Running experiment: A Healthy Service
<span class="token green">[2021-07-22 09:32:16 INFO]</span> Steady-state strategy: default
<span class="token green">[2021-07-22 09:32:16 INFO]</span> Rollbacks strategy: default
<span class="token green">[2021-07-22 09:32:16 INFO]</span> No steady state hypothesis defined. That's ok, just exploring.
<span class="token green">[2021-07-22 09:32:16 INFO]</span> Playing your experiment's method now...
<span class="token green">[2021-07-22 09:32:16 INFO]</span> Action: send_good_indicator
<span class="token green">[2021-07-22 09:32:16 INFO]</span> Let's rollback...
<span class="token green">[2021-07-22 09:32:16 INFO]</span> No declared rollbacks, let's move on.
<span class="token green">[2021-07-22 09:32:16 INFO]</span> Experiment ended with status: completed
```

As you can see, the experiment ran successfully!

### Observing your good reliability

Take a look at the terminal window where you ran `reliably slo report -w`, you should see something like:

```reliably
<span class="token purple">Refreshing SLO report every 3 seconds.</span> Press CTRL+C to quit.
                                                        <span class="token purple bold">Current  Objective  / Time Window     Type             Trend</span>
  Service #1: exploring-reliability-guide-service
  ✅ 99.9% of our requests are in the 2xx class         <span class="token green">100.00%</span>      99.9%  / 1h0m0s          Availability     <span class="token green">✓</span>
```

Awesome! You've successfully got a `Good` service. You can see that your current availability is `100%` and that you've had one indicator pushed as shown by `✓` under `Trend`

## Getting bad reliability

Now that you've seen what `Good` looks like, it's time to see what `Bad` looks like. We've already run through the experiment format in the previous section, so we'll just give
you the code to copy for this part.

### The experiment

Copy this experiment into a file called `unhealthy-experiment.json`:

```json
{
    "version": "1.0.0",
    "title": "An Unhealthy Service",
    "description": "Sends Reliably `Bad` Indicators to mimic an unhealthy service",
    "method": [
        {
            "type": "action",
            "name": "send_bad_indicator",
            "provider": {
                "type": "python",
                "module": "reliability_utils",
                "func": "send_bad_indicator",
                "arguments": {}
            }
        }
    ]
}
```
<CopyToClipboard />

#### `reliability_utils.send_bad_indicator`

Copy the following code into `reliability_utils.py`, below `send_good_indicator`:

```python
def send_bad_indicator(
    configuration: Configuration = None, secrets: Secrets = None
) -> None:
    """
    For a given TOKEN and ORG, send a 90% availability Indicator
    for the selector that matches `category=Availability` and
    `indicator_name=exploring-reliability-guide-service-availability-indicator`
    """
    timenow = datetime.utcnow().isoformat() + 'Z'
    body = {
        "metadata": {
            "labels": {
                "category": "Availability",
                "indicator_name": "exploring-reliability-guide-service-availability-indicator",
            }
        },
        "spec": {"from": timenow, "to": timenow, "percent": 90.0},
    }

    requests.put(
        url=f"https://api.reliably.com/entities/{ORG}/reliably.com/v1/indicator",
        data=json.dumps(body),
        headers={"Authorization": f"Bearer {TOKEN}"},
    )
```
<CopyToClipboard />

You'll also need to replace `__all__ = ["send_good_indicator"]` with:

```python
__all__ = ["send_good_indicator", "send_bad_indicator"]
```
<CopyToClipboard />

### Viewing the SLO Report

In a new terminal window (or the same one if you've not closed it), run the following:

```reliably
<span class="token dollar"></span>reliably slo report -w
```
<CopyToClipboard />

```reliably
<span class="token purple">Refreshing SLO report every 3 seconds.</span> Press CTRL+C to quit.
                                                        <span class="token purple bold">Current  Objective  / Time Window     Type             Trend</span>
  Service #1: exploring-reliability-guide-service
  ✅ 99.9% of our requests are in the 2xx class         <span class="token green">100.00%</span>      99.9%  / 1h0m0s          Availability     <span class="token green">✓</span>
```

This will keep the SLO report running so that we can see the `Bad` indicator reaching Reliably when we run the experiment. You'll notice we can see the `Good` indicator from earlier.

### Running the unhealthy experiment

In a different terminal window from the `reliably slo report` one, run the following:

```reliably
<span class="token dollar"></span>PYTHONPATH=. chaos run unhealthy-experiment.json
```
<CopyToClipboard />

```reliably
<span class="token green">[2021-07-22 10:28:32 INFO]</span> Validating the experiment's syntax
<span class="token green">[2021-07-22 10:28:32 INFO]</span> Experiment looks valid
<span class="token green">[2021-07-22 10:28:32 INFO]</span> Running experiment: An Unhealthy Service
<span class="token green">[2021-07-22 10:28:32 INFO]</span> Steady-state strategy: default
<span class="token green">[2021-07-22 10:28:32 INFO]</span> Rollbacks strategy: default
<span class="token green">[2021-07-22 10:28:32 INFO]</span> No steady state hypothesis defined. That's ok, just exploring.
<span class="token green">[2021-07-22 10:28:32 INFO]</span> Playing your experiment's method now...
<span class="token green">[2021-07-22 10:28:32 INFO]</span> Action: send_bad_indicator
<span class="token green">[2021-07-22 10:28:33 INFO]</span> Let's rollback...
<span class="token green">[2021-07-22 10:28:33 INFO]</span> No declared rollbacks, let's move on.
<span class="token green">[2021-07-22 10:28:33 INFO]</span> Experiment ended with status: completed
```

As you can see, the experiment ran successfully!

### Observing your bad reliability

Take a look again at the terminal window where you ran `reliably slo report -w`, you should see something like:

```reliably
<span class="token purple">Refreshing SLO report every 3 seconds.</span> Press CTRL+C to quit.
                                                        <span class="token purple bold">Current  Objective  / Time Window     Type             Trend</span>
  Service #1: exploring-reliability-guide-service
  ❌ 99.9% of our requests are in the 2xx class          <span class="token red">90.00%</span>      99.9%  / 1h0m0s          Availability     <span class="token green">✓</span> <span class="token red">✕</span>
```

Oh dear! You've successfully got a `Bad` service. You can see that your current availability is `90%` and that you've had two indicators pushed as shown by `✓ ✕` under `Trend`

## Using your SLOs as a Steady State Hypothesis

Now that you can observe the reliability of your 'system' and conduct Chaos Engineering experiments against it, it's a good time to further integrate Reliably and Chaos Toolkit!

Earlier, you installed `chaostoolkit-reliably`, this extension of Chaos Toolkit provides functionality that allows you to hook into Reliably's SLOs and use them as your Steady State Hypothesis.
Using it, you can conduct Chaos Engineering experiments and verify whether your system's reliability has degraded during them.

More information on [Steady State Hypothesis](https://chaostoolkit.org/reference/api/experiment/#steady-state-hypothesis) is available on the Chaos Toolkit website.

### Setting up a Steady State Hypothesis

Below is a Steady State Hypothesis for this guide, you should copy it into `healthy-experiment.json`, just above `method`.

```json
"steady-state-hypothesis": {
    "title": "We do not fail our SLO when conducting an experiment",
    "probes": [
        {
            "name": "SLO is met",
            "type": "probe",
            "provider": {
                "type": "python",
                "module": "chaosreliably.slo.probes",
                "func": "slo_is_met",
                "arguments": {
                    "labels": {
                        "name": "99.9% of our requests are in the 2xx class",
                        "service": "exploring-reliability-guide-service"
                    }
                }
            },
            "tolerance": true
        }
    ]
},
```
<CopyToClipboard />

This statement tells Chaos Toolkit that you define your Steady State as being your SLO you defined previously with Reliably.

You identify the SLO with the labels within the manifest, in this case:

```yaml
metadata:
  labels:
    name: 99.9% of our requests are in the 2xx class
    service: exploring-reliability-guide-service
```

within your manifest translates to the following in your experiment:

```json
"labels": {
    "name": "99.9% of our requests are in the 2xx class",
    "service": "exploring-reliability-guide-service"
},
```

### Seeing your reliability continue

#### Getting to `Good` first
Before you run the experiment and validate that your SLOs are met during the experiment, you need to put the 'system' back into a `Good` state.

You can do this by running:

```reliably
<span class="token dollar"></span>PYTHONPATH=. chaos run healthy-experiment.json --hypothesis-strategy=after-method-only
```
<CopyToClipboard />

```reliably
<span class="token green">[2021-07-27 16:25:38 INFO]</span> Validating the experiment's syntax
<span class="token green">[2021-07-27 16:25:38 INFO]</span> Experiment looks valid
<span class="token green">[2021-07-27 16:25:38 INFO]</span> Running experiment: A Healthy Service
<span class="token green">[2021-07-27 16:25:38 INFO]</span> Steady-state strategy: after-method-only
<span class="token green">[2021-07-27 16:25:38 INFO]</span> Rollbacks strategy: default
<span class="token green">[2021-07-27 16:25:38 INFO]</span> Playing your experiment's method now...
<span class="token green">[2021-07-27 16:25:38 INFO]</span> Action: send_good_indicator
<span class="token green">[2021-07-27 16:25:39 INFO]</span> Steady state hypothesis: We do not fail our SLO when conducting an experiment
<span class="token green">[2021-07-27 16:25:39 INFO]</span> Probe: SLO is met
<span class="token green">[2021-07-27 16:25:39 INFO]</span> All Objective Results were OK.
<span class="token green">[2021-07-27 16:25:39 INFO]</span> Steady state hypothesis is met!
<span class="token green">[2021-07-27 16:25:39 INFO]</span> Let's rollback...
<span class="token green">[2021-07-27 16:25:39 INFO]</span> No declared rollbacks, let's move on.
<span class="token green">[2021-07-27 16:25:39 INFO]</span> Experiment ended with status: completed
```

All this does is sends a `Good` indicator to Reliably. The `--hypothesis-strategy=after-method-only` flag tells Chaos Toolkit that we shouldn't fail on the `Bad` state at the start.

It will only check the hypothesis **after** your `method` has run.

#### Confirming `Good` continues with the healthy experiment

Now you can run your experiment **with** validation of your Steady State Hypothesis:

```reliably
<span class="token dollar"></span>PYTHONPATH=. chaos run healthy-experiment.json
```
<CopyToClipboard />

```reliably
<span class="token green">[2021-07-27 16:30:14 INFO]</span> Validating the experiment's syntax
<span class="token green">[2021-07-27 16:30:14 INFO]</span> Experiment looks valid
<span class="token green">[2021-07-27 16:30:14 INFO]</span> Running experiment: A Healthy Service
<span class="token green">[2021-07-27 16:30:14 INFO]</span> Steady-state strategy: default
<span class="token green">[2021-07-27 16:30:14 INFO]</span> Rollbacks strategy: default
<span class="token green">[2021-07-27 16:30:14 INFO]</span> Steady state hypothesis: We do not fail our SLO when conducting an experiment
<span class="token green">[2021-07-27 16:30:14 INFO]</span> Probe: SLO is met
<span class="token green">[2021-07-27 16:30:14 INFO]</span> All Objective Results were OK.
<span class="token green">[2021-07-27 16:30:14 INFO]</span> Steady state hypothesis is met!
<span class="token green">[2021-07-27 16:30:14 INFO]</span> Playing your experiment's method now...
<span class="token green">[2021-07-27 16:30:14 INFO]</span> Action: send_good_indicator
<span class="token green">[2021-07-27 16:30:14 INFO]</span> Steady state hypothesis: We do not fail our SLO when conducting an experiment
<span class="token green">[2021-07-27 16:30:14 INFO]</span> Probe: SLO is met
<span class="token green">[2021-07-27 16:30:15 INFO]</span> All Objective Results were OK.
<span class="token green">[2021-07-27 16:30:15 INFO]</span> Steady state hypothesis is met!
<span class="token green">[2021-07-27 16:30:15 INFO]</span> Let's rollback...
<span class="token green">[2021-07-27 16:30:15 INFO]</span> No declared rollbacks, let's move on.
<span class="token green">[2021-07-27 16:30:15 INFO]</span> Experiment ended with status: completed
```

As you can see from the above output, your experiment has done the following:

* Checked your Steady State Hypothesis **before** running your method ✅
* Played your experiments method (Send a good indicator) ✉️
* Checked your Steady State Hypothesis **after** running your method ✅

### Seeing your reliability degrade

#### Update `unhealthy-experiment.json` with your hypothesis

Firstly, you'll need to copy the hypothesis block below into `unhealthy-experiment.json`, like you did with `healthy-experiment.json`:

```json
"steady-state-hypothesis": {
    "title": "We do not fail our SLO when conducting an experiment",
    "probes": [
        {
            "name": "SLO is met",
            "type": "probe",
            "provider": {
                "type": "python",
                "module": "chaosreliably.slo.probes",
                "func": "slo_is_met",
                "arguments": {
                    "labels": {
                        "name": "99.9% of our requests are in the 2xx class",
                        "service": "exploring-reliability-guide-service"
                    }
                }
            },
            "tolerance": true
        }
    ]
},
```
<CopyToClipboard />

#### Running the unhealthy experiment with your hypothesis

You can now also see that the unhealthy experiment will fail by running:

```reliably
<span class="token dollar"></span>PYTHONPATH=. chaos run unhealthy-experiment.json
```
<CopyToClipboard />

```reliably
<span class="token green">[2021-07-27 16:35:39 INFO]</span> Validating the experiment's syntax
<span class="token green">[2021-07-27 16:35:40 INFO]</span> Experiment looks valid
<span class="token green">[2021-07-27 16:35:40 INFO]</span> Running experiment: An Unhealthy Service
<span class="token green">[2021-07-27 16:35:40 INFO]</span> Steady-state strategy: default
<span class="token green">[2021-07-27 16:35:40 INFO]</span> Rollbacks strategy: default
<span class="token green">[2021-07-27 16:35:40 INFO]</span> Steady state hypothesis: We do not fail our SLO when conducting an experiment
<span class="token green">[2021-07-27 16:35:40 INFO]</span> Probe: SLO is met
<span class="token green">[2021-07-27 16:35:40 INFO]</span> All Objective Results were OK.
<span class="token green">[2021-07-27 16:35:40 INFO]</span> Steady state hypothesis is met!
<span class="token green">[2021-07-27 16:35:40 INFO]</span> Playing your experiment's method now...
<span class="token green">[2021-07-27 16:35:40 INFO]</span> Action: send_bad_indicator
<span class="token green">[2021-07-27 16:35:40 INFO]</span> Steady state hypothesis: We do not fail our SLO when conducting an experiment
<span class="token green">[2021-07-27 16:35:40 INFO]</span> Probe: SLO is met
<span class="token red">[2021-07-27 16:35:40 CRITICAL]</span> The following Objective Results were not OK:

    Objective Results are sorted by latest at the top:
    | From                                 | To                                   |   Objective % |   Actual % |   Remaining % | Indicator Selector                                                                                           |
    |--------------------------------------|--------------------------------------|---------------|------------|---------------|--------------------------------------------------------------------------------------------------------------|
    | 2021-07-27 15:35:40.268235 +0000 UTC | 2021-07-27 15:35:40.268235 +0000 UTC |          99.9 |         90 |          -9.9 | {'category': 'Availability', 'indicator_name': 'exploring-reliability-guide-service-availability-indicator'} |
<span class="token red">[2021-07-27 16:35:40 CRITICAL]</span> Steady state probe 'SLO is met' is not in the given tolerance so failing this experiment
<span class="token green">[2021-07-27 16:35:40 INFO]</span> Experiment ended with status: deviated
<span class="token green">[2021-07-27 16:35:40 INFO]</span> The steady-state has deviated, a weakness may have been discovered
```

As you can see from the above Chaos Toolkit output, your experiment has ended with the status of `deviated`.

The experiment has done the following:

* Checked your Steady State Hypothesis **before** running your method ✅
* Played your experiment's method (Send a bad indicator) ✉️
* Checked your Steady State Hypothesis **after** running your method ❌

The `chaostoolkit-reliably` extension also provides some output which indicates to you _what_ Result caused the deviation and what its actual percentage was compared to your Objectives.

## Tieing it all up

Let's conclude on what you've covered in the above sections:

* You've defined your reliability with an [Objective](#define-your-objective)
* You've observed your reliability with [`reliably slo report`](#observe-your-system)
* You've created both a [healthy](#create-a-chaos-engineering-experiment) and an [unhealthy](#the-experiment) experiment with Chaos Toolkit
* You've observed both [good](#observing-your-good-reliability) and [bad](#observing-your-bad-reliability) reliability of your 'system'
* You've explored the impact on your Steady State Hypothesis (and importantly your reliability) with both [healthy](#seeing-your-reliability-continue) and [unhealthy](#seeing-your-reliability-degrade) experiments

You'll want to clear up after yourself and remove the Objective that was defined, this is so that it no longer appears in your reports.

You can delete the objective by running:

```reliably
<span class="token dollar"></span>reliably slo delete --selector "service=exploring-reliability-guide-service"
```
<CopyToClipboard />

At this point, you should be comfortable with how you might integrate your own Reliably SLOs created for your system, with your Steady State Hypothesis in your Chaos Toolkit experiments. 

This all ultimately enables you to run chaos engineering experiments against your systems and see the impact they have on the things that **really** matter: what your users experience.
