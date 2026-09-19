---
id: BUG-023
title: "Audio Effects Fail to Trigger Following Network Disconnection and Reconnection"
game: BitCraft Online
company: Clockwork Labs
category: "Audio / System Mechanics"
severity: Medium
status: Submitted
---

# BUG-023: Audio Effects Fail to Trigger Following Network Disconnection and Reconnection

## Problem Description
If the game client loses connection to the server and successfully reconnects, most ambient and action-based audio cues stop playing entirely. 

While background music and UI interactions may persist, character action sound effects—most notably gathering, harvesting, and crafting audio loops—fail to trigger until the client is fully restarted.

---

## Steps to Reproduce
1. Launch the game and initiate any gathering or crafting activity to verify sound effects are playing normally.
2. Simulate or undergo a network disconnection event (e.g., toggling network adapter or experiencing temporary latency drop) until the client triggers a reconnecting/reconnected flow.
3. Once back in the world, perform gathering or crafting interactions.
4. Observe that the corresponding action sound effects fail to play.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | Audio engine states and event listeners should re-initialize seamlessly upon reconnection, preserving full gameplay sound effects. |
| **Actual Result** | Action-based audio cues (gathering, crafting, combat) permanently mute for the rest of the session after a reconnection event. |

---

## Technical Observations & Potential Causes
* **Audio Event Listener Unhooking:** The client audio manager or sound bank listener state may fail to re-bind to local entity animation events upon reconnecting to the spatial server instance.
* **FMOD / Audio Engine Instance Desync:** The session reset during network recovery might terminate active audio instances or bus channels without properly re-instantiating them for subsequent action triggers.
