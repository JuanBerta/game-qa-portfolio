---
id: BUG-008
title: "Transient Game Engine Freeze and Telemetry Stutter Upon Toggling Window Focus (Alt-Tab)"
game: BitCraft Online
company: Clockwork Labs
category: "Performance / Engine & Window Focus"
severity: Medium
status: Submitted
---

# BUG-008: Transient Game Engine Freeze and Telemetry Stutter Upon Toggling Window Focus (Alt-Tab)

## Problem Description
When toggling window focus away from or back to the game client (via `Alt + Tab`), the game client experiences a temporary freeze/hitch in processing loop execution. 

During this brief window freeze, client-side game state updates and outgoing telemetry packets stall. This engine hitch causes active timed interactions (such as gathering or crafting actions) to briefly pause processing locally, leading to false-positive idle signals on external monitoring utilities and client-side input desyncs upon returning focus.

---

## Steps to Reproduce
1. Launch **BitCraft Online** and initiate a continuous channelled or repetitive action (e.g., gathering resources or crafting).
2. Switch window focus back and forth between the game client and another application using `Alt + Tab`.
3. Observe the client frame pipeline briefly hitch/freeze during the focus transition event.
4. Note that client event emission and local state execution halt momentarily until the application window regains active OS thread execution.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | The client game engine should handle window focus transitions asynchronously without freezing main thread execution or interrupting outgoing state telemetry updates. |
| **Actual Result** | Toggling window focus causes a temporary client-side freeze that halts frame rendering and stalls event packet dispatching. |

---

## Technical Observations & Potential Causes
* **Main Thread Blocking on Window Event:** The application loop may be synchronously blocking on `OnApplicationFocus` or OS display context switches, pausing active thread execution until the window manager completes the focus shift.
* **Background Process Throttling Aggression:** Client resource-throttling limits applied when the window is unfocused may be executing too aggressively on the primary tick thread, interrupting smooth tick processing and telemetry dispatch.
