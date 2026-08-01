---
id: BUG-014
title: "Gathering Cancels Intermittently After Logging In Mounted on a Deployable"
game: BitCraft Online
company: Clockwork Labs
category: "Gameplay / Mounts & Resource Gathering"
severity: Medium
status: Submitted
---

# BUG-014: Gathering Cancels Intermittently After Logging In Mounted on a Deployable

## Problem Description
If a player logs out while mounted on a deployable and subsequently logs back in, attempting to gather resources while remaining mounted will cause the gathering action to fail. 

The character performs the initial gathering animation once, after which the channelled action cancels automatically. Dismounting from the deployable and remounting acts as a temporary workaround to restore normal gathering behavior.

---

## Steps to Reproduce
1. Mount any deployable container or vehicle.
2. Log off the game while remaining mounted.
3. Log back into the game server.
4. Approach a gatherable resource node and attempt to start gathering while still mounted.
5. Observe that the character completes the first cycle/animation frame of the gather action, then immediately cancels the channelled action.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | Logging in while mounted should preserve full character functionality, allowing uninterrupted gathering actions while mounted. |
| **Actual Result** | The gathering channel cancels after a single animation cycle until the player manually dismounts and remounts the deployable. |

---

## Technical Observations & Potential Causes
* **Mount State Desync on Session Initialization:** The client session initialization routine may attach the player model visually to the deployable without fully instantiating the mounted gathering state handlers on the server side.
* **Missing Action Flags on Re-entry:** The character's active flags upon logging in may miss the required "Mounted Gathering Allowed" state validation, causing the server to reject consecutive gathering tick requests and cancel the loop.
