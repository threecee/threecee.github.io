---
title: Troubleshooting
description: Common issues with HealthInsights and MyLoop With Watch, and what to do.
---

# Troubleshooting

Common issues, in rough order of how likely you'll hit each one.

## TestFlight install failed

**Symptom:** the link in the email gives an error, or "Accept" is
greyed out in TestFlight.

**Likely cause:** the invite has expired. TestFlight invites expire
after 90 days.

**Fix:** ask Carl to re-invite. The new invite arrives in your inbox
within a minute or two.

## App crashes on launch

**Likely cause:** HealthKit permissions were denied or never granted.

**Fix:** open iOS **Settings → Privacy & Security → Health → \[app
name\]** and grant the requested categories. Then re-launch the app.

## MyLoop watch app doesn't appear on the watch

**Likely cause:** the watch hasn't synced the embedded watch app yet,
or the watch isn't paired/connected.

**Fix:** open the **Watch** app on your iPhone → main page → confirm
your watch shows as connected. Scroll to **"Available Apps"** → find
**MyLoop With Watch** → tap **Install**. If still not appearing after a
few minutes, restart your iPhone, then your watch.

## Pod won't pair

**Likely causes (in order):**
1. The pod was previously paired to another phone or watch and is
   still bonded there.
2. The pod is too far from the device (try within 1 meter for pairing).
3. The pod is faulty.

**Fix:** unpair from the previous device first. If unsure, deactivate
the pod (Loop offers a "deactivate" action) and start fresh with a new
pod.

## Alerts not firing during Focus mode

**Likely cause:** the Critical Alerts entitlement for MyLoop is pending
Apple approval. Until approved, alerts respect Focus modes (so they
don't always interrupt).

**Fix:** add MyLoop With Watch to the **Allowed Notifications** list
in your Focus mode settings. As a backup, the watch's haptic alerts
fire regardless of Focus.

## Watch shows "Loop warming up" forever

**Likely cause:** the watch became the driver but couldn't complete a
full Loop iteration (typically because the pod is out of range, or
because Nightscout creds are missing and the watch's first iteration
needs them).

**Fix:** confirm the pod is within range of the watch (typically wear
the watch on the same arm or near the pod). Open the MyLoop watch app
and wait 5–10 minutes for the next iteration. If the badge persists,
manually trigger handoff back to the phone and re-test.

## "Who's driving" indicator is missing or stuck

**Fix:** force-quit the app on whichever device shows the wrong state
(double-press digital crown on watch, swipe away on phone), then
re-open. If still stuck after both devices are restarted, contact Carl.

## When in doubt

Fall back to manual insulin delivery (basal pen + bolus syringe) and
contact Carl. Loop is helpful but never load-bearing — your manual
backup is always the safest option.

_Last updated: 2026-05-01_
