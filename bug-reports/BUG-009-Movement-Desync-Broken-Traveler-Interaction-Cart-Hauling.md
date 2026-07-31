---
id: BUG-009
title: "Movement Speed Desync and Broken NPC Interaction Menu When Right-Clicking Travelers While Hauling Carts"
game: BitCraft Online
company: Clockwork Labs
category: "Controls / Movement & NPC Interaction"
severity: Medium
status: Submitted
---

# BUG-009: Movement Speed Desync and Broken NPC Interaction Menu When Right-Clicking Travelers While Hauling Carts

## Problem Description
While actively hauling a cart or deployable, repeatedly right-clicking a Traveler NPC from a distance causes micro speedups and movement stutter (server/client position desynchronization). 

Additionally, once the player character reaches the Traveler NPC and the interaction interface opens, the options/buttons within the dialogue menu become unresponsive, blocking NPC interaction until the cart is released or the interaction is reset.

---

## Steps to Reproduce
1. Attach and begin hauling a cart or deployable container.
2. Locate a Traveler NPC in the world and stand at a distance.
3. Rapidly right-click on the Traveler NPC to initiate an approach/interaction command.
4. Observe micro speedups/teleportation hitches as the character approaches the NPC.
5. Wait for the character to reach interaction range and observe the Traveler dialogue window open.
6. Click on any of the presented interaction options/buttons in the NPC menu and observe that they fail to execute or respond.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | Hauling a cart toward an NPC should maintain standard movement speed without position desync, and opening the Traveler interaction menu should allow normal menu option selection. |
| **Actual Result** | Rapidly issuing interaction commands while hauling triggers movement speed desync hitches and leaves the resulting NPC interaction menu buttons completely unresponsive. |

---

## Technical Observations & Potential Causes
* **State Machine & Speed Modifier Conflict:** Rapidly re-issuing interaction pathfinding requests while under the movement-speed penalty of hauling a cart may cause the client movement prediction model to briefly desync with server position validation, creating position snap-forwards (micro speedups).
* **UI Event Listener Lock:** The interaction state machine may fail to cleanly transition into the "Interacting" state while the player character is still flagged as "Hauling," resulting in an unhandled UI state where the dialogue window renders visually but input event handlers remain disabled.
