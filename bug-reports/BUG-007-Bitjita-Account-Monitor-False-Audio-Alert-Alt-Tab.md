---
id: BUG-007
title: "Account Monitor Audio Cue Triggers Falsely on Window Focus Toggle (Alt-Tab)"
game: Bitcraft Online
tool: Bitjita (Third-Party)
category: "Account Monitor / Sound & Session State"
severity: Medium
status: Submitted
---

# BUG-007: Account Monitor Audio Cue Triggers Falsely on Window Focus Toggle (Alt-Tab)

## Problem Description
In the Bitjita Account Monitor, using the **"Gathering"** default preset (which triggers an idle alert when no experience is gained after 2 seconds) produces false positive audio alerts when the player frequently toggles focus (`Alt + Tab`) between BitCraft and other applications.

Because the game client throttles its frame rate/resource allocation when running in the background, client-side packet timing or polling updates lag briefly during window switches. The Account Monitor interprets this temporary telemetry delay as inactivity—firing the idle sound cue multiple times—even though the game server is actively processing character actions.

---

## Steps to Reproduce
1. Navigate to **Bitjita -> Account Monitor**.
2. Select the **"Gathering"** monitoring preset (configured with an *"XP Idle after 2 seconds"* rule).
3. Begin a gathering action in BitCraft that grants experience over time.
4. Rapidly or repeatedly switch window focus away from and back to the game client (`Alt + Tab`).
5. Observe that the idle sound cue fires repeatedly during window switching, despite the game continuous activity.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | The Account Monitor sound cue should only trigger when the player has legitimately stopped gaining XP for more than 2 seconds, accounting for background window throttling. |
| **Actual Result** | The audio alert triggers falsely multiple times during window focus switches while the player is still actively receiving XP on the server. |

---

## Technical Observations & Potential Causes
* **Client Throttling / Polling Delay:** When the game loses window focus, frame-rate throttling delays client-side API/telemetry updates. Bitjita's monitor perceives this gap in incoming data packets as zero-XP progression, prematurely tripping the 2-second timeout threshold.
* **Lack of De-bounce / Hysteresis Buffer:** The idle detection logic lacks a grace period or hysteresis buffer to filter out transient telemetry delays caused by browser/OS focus events before triggering the audio alert.
