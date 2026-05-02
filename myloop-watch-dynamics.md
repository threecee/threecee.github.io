---
title: Watch dynamics
description: How MyLoop With Watch divides work between iPhone and Apple Watch — handoff, who's driving, warming-up.
---

# Watch dynamics

This page explains the genuinely novel behavior of MyLoop With Watch:
how the iPhone and the Apple Watch divide responsibility for talking to
the pod and running the Loop algorithm. None of this exists in vanilla
Loop.

## The big idea: one driver at a time

At any given moment, exactly one device is the **driver** — the device
that has an active Bluetooth connection to your pod and runs the Loop
algorithm. The other device is the **passenger** — it shows status but
doesn't talk to the pod and doesn't compute doses.

The two states:

- **Phone-driving** (the default): your iPhone is in range of the pod
  (typically within ~10 meters / 30 feet). iPhone runs Loop every five
  minutes. The watch shows the latest glucose + IOB but defers to the
  phone.
- **Watch-driving**: your iPhone is out of range or off, and the watch
  has taken over. Watch runs Loop every five minutes. Watch alerts fire
  on your wrist.

### How to tell which device is driving

Look at the loop status ring on either device:

- **A small white dot in the center of the ring** = "this device is
  currently driving."
- **No dot in the center** = "the other device is driving" (this device
  is the passenger).

The dot **pulses gently** for the brief sub-second window during which
ownership is being handed off between phone and watch.

Same convention on both devices, so you always read the indicator
locally: "is my phone driving?" check the iPhone's loop ring; "is my
watch driving?" check the Apple Watch's loop ring. If both rings show a
dot at the same time during normal operation, that's a split-brain
condition the system detects and resolves automatically (phone wins).

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 1rem; max-width: 600px; margin: 1.5rem 0;">

<figure style="margin: 0; text-align: center;">
<img src="images/driver-iphone-phone-driving.png" alt="iPhone with phone driving — dot visible" style="width: 100%;">
<figcaption><strong>iPhone</strong> — phone driving (dot)</figcaption>
</figure>

<figure style="margin: 0; text-align: center;">
<img src="images/driver-iphone-watch-driving.png" alt="iPhone with watch driving — no dot" style="width: 100%;">
<figcaption><strong>iPhone</strong> — watch driving (no dot)</figcaption>
</figure>

<figure style="margin: 0; text-align: center;">
<img src="images/driver-watch-watch-driving.png" alt="Apple Watch with watch driving — dot visible" style="width: 100%;">
<figcaption><strong>Apple Watch</strong> — watch driving (dot)</figcaption>
</figure>

<figure style="margin: 0; text-align: center;">
<img src="images/driver-watch-phone-driving.png" alt="Apple Watch with phone driving — no dot" style="width: 100%;">
<figcaption><strong>Apple Watch</strong> — phone driving (no dot)</figcaption>
</figure>

</div>

_Mockups above show only the ring and indicator; the live HUD includes glucose, IOB, and other status around it. Real on-device screenshots will replace these after hardware verification._

## Handoff: how the watch takes over

Handoff is the moment when the driver role moves from one device to the
other. Two paths trigger it:

1. **Automatic, on phone disconnect.** When the phone has been
   out of Bluetooth range of the pod for several minutes, the watch
   notices, requests the BLE bond, and takes over. This is the typical
   bedtime case.
2. **Manual, in the watch app.** You can initiate a handoff from the
   watch's settings. Useful for testing, or for cases where you want
   the watch to take over before walking out of range.

When handoff happens, the BLE connection physically moves from the phone
to the watch. The bonding-handoff orchestrator in MyLoop ensures only
one device owns the bond at a time, so the pod never sees conflicting
commands.

## Warming up: the first few iterations after handoff

When the watch becomes the driver, its Loop history is colder than the
phone's was. The watch backfills recent glucose from the CGM and recent
dose events from the pod, but for the first **~30 minutes (about 5
algorithm iterations)** it operates with a smaller history window.

During this window, the watch displays a small **"Loop warming up"**
badge. While the badge is showing:

- The algorithm is running, but on conservative defaults.
- Closed-loop dosing decisions are smaller / more cautious than they
  would be with full history.
- Glucose alerts fire normally.

After the warm-up window completes, the badge clears and the watch
operates with a full algorithm context.

## What happens when phone + watch are separated

The intended scenario: you go to bed with your phone on the bedside
table, then leave the room. Your watch stays on your wrist. As you walk
away, the phone loses its BLE connection to the pod; the watch detects
this and initiates handoff. Within a few minutes, the watch is the
driver and Loop continues uninterrupted.

While you're separated:
- Glucose continues to update on the watch.
- Dosing decisions continue, computed on the watch.
- Alerts fire on your wrist.
- The phone may show "watch is currently driving" if you check it.

## Reverting to phone-driving

When you return and the phone is reachable from the watch over Apple's
WCSession transport for **at least 60 seconds**, the reverse handoff
fires automatically: the phone takes the BLE bond back, and the watch
reverts to passenger. The 60-second debounce avoids flapping during
brief reconnect storms.

Same warming-up window applies in reverse — the phone's first
iteration after taking back the role uses its existing history, so
warming up is usually not visible.

The auto-revert behavior is governed by the handoff mode setting
(default: `automatic`). If you set the mode to `manual`, the watch
keeps the driver role until you initiate a handoff back to the phone
explicitly via the watch's settings.

## What to do if handoff doesn't happen

If you check the watch and the badge says it's still in passenger
mode after the phone has clearly gone out of range:

1. Wake the watch and open the MyLoop app.
2. Wait 30–60 seconds for the watch to detect the disconnect.
3. If still no handoff, manually initiate handoff via the watch's
   settings (see [Troubleshooting](/troubleshooting) for the gesture
   path).
4. If manual handoff also fails, fall back to manual insulin delivery
   and contact Carl.

## What is NOT yet supported

- Algorithm-level differences between phone and watch (the watch runs
  the same Loop algorithm with the same settings; nothing diverges).
- Multiple pods at once (one pod, one driver at a time).
- Handoff to a non-paired second iPhone (only paired Apple Watch).
- Critical Alerts on the watch when in Focus modes — this entitlement
  is pending Apple approval; for now use Focus exemptions or rely on
  the watch's haptic alerts.

_Last updated: 2026-05-02_

_Watch behavior verified on hardware: pending. Auto-revert from watch
back to phone (Reverting to phone-driving section above) shipped in
Build 860 — earlier builds had the path stubbed out and the watch held
the driver role until manual user action. Update this footer when
verified on real devices._
