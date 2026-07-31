---
id: BUG-011
title: "Active Crafting Process Interrupts Upon Reopening Crafting Station Interface"
game: BitCraft Online
company: Clockwork Labs
category: "Crafting / Station UI & Interaction"
severity: Medium
status: Submitted
---

# BUG-011: Active Crafting Process Interrupts Upon Reopening Crafting Station Interface

## Problem Description
When a crafting batch is actively running at a crafting station, opening that station's interaction menu will intermittently interrupt and halt the active crafting progress. 

Re-engaging the station UI resets or cancels the ongoing queue state, requiring the player to restart or resume the crafting operation manually.

---

## Steps to Reproduce
1. Approach any crafting station and queue up a batch of items to begin active crafting.
2. Step away or wait a short moment while the craft is actively processing.
3. Interact with the same crafting station to open its menu interface again.
4. Observe that the active crafting progress immediately stops/cancels upon UI load.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | The crafting process should continue running seamlessly in the background or remain active while the station UI is open. |
| **Actual Result** | The active crafting process is interrupted and stops completely as soon as the station menu is opened. |

---

## Technical Observations & Potential Causes
* **State Machine Reset on Interaction:** Interacting with the crafting station may trigger a state machine transition that inadvertently clears or resets the station's active worker thread/queue handler.
* **Client-Server State Sync Conflict:** Opening the station UI requests a fresh state payload from the server, which may override and zero out local client-side progress timers for active craft jobs.

---

## Environment & Metadata
* **Platform:** PC / Steam
* **Build / Game Version:** `Early-Access-2-c354e832`
* **Reproduction Rate:** ~3/5 (Intermittent)
