---
title: MyLoop
description: What MyLoop With Watch does and how it differs from vanilla Loop.
---

# MyLoop With Watch

Carl's personal fork of the open-source **Loop** closed-loop insulin
delivery app, with an Apple Watch companion. Distributed via TestFlight
to immediate family only.

## What it does

Loop is a closed-loop insulin delivery system. It reads your glucose
from a CGM (Dexcom G7), computes how much insulin you need every five
minutes, and commands your Omnipod pump to deliver it. You set targets
and meal carbs; Loop handles the rest.

The original Loop runs only on the iPhone. **MyLoop With Watch adds an
Apple Watch companion that takes over when your phone is far from the
pod** — most commonly overnight, when you're asleep with the phone in
another room.

## How it differs from vanilla Loop

| | Vanilla Loop | MyLoop With Watch |
|---|---|---|
| iOS app runs Loop algorithm | ✓ | ✓ |
| Watch app shows status | ✓ | ✓ |
| **Watch app runs Loop algorithm** | — | ✓ |
| **Watch can command the pump directly** | — | ✓ |
| **Pod handover phone↔watch** | — | ✓ |
| Nightscout sync | iOS only | iOS + watch |

The new behavior — watch self-driving, pod handover, and the warming-up
state — is genuinely novel and worth understanding.
**See [Watch dynamics](/myloop-watch-dynamics)** for the deep dive.

## Closed-loop vocabulary you should know

If you're new to Loop, the Loop community maintains authoritative docs
for closed-loop insulin delivery concepts (basal, bolus, IOB, COB, ISF,
etc.) — search "LoopDocs" or "Loop and Learn" for the current site.
MyLoop is feature-compatible with vanilla Loop on those concepts.

## Liability and informed consent

**MyLoop With Watch is a personal fork of community-maintained
open-source software. The Loop algorithm has not been reviewed or
approved by the FDA, EMA, or any other regulatory body.** This app is
for personal use by individuals who understand the risks of using
non-regulated closed-loop insulin delivery software.

**Do not use this app without consulting your endocrinologist and your
care team.** If anything behaves unexpectedly, fall back to manual
insulin delivery (your own basal + bolus pen or syringe) until you can
diagnose the problem with Carl's help.

## Privacy

See the [MyLoop With Watch privacy
policy](https://threecee.github.io/loop-privacy/).

_Last updated: 2026-05-01_
