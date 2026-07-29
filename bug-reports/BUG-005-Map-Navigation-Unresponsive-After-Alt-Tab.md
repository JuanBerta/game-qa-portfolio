---
id: BUG-005
title: "Map Navigation Inputs Unresponsive After Repeated Window Focus Toggles (Alt-Tab)"
game: BitCraft Online
company: Clockwork Labs
category: "Controls / Window Focus & Input"
severity: Medium
status: Submitted
---

# BUG-005: Map Navigation Inputs Unresponsive After Repeated Window Focus Toggles (Alt-Tab)

## Problem Description
When frequently toggling focus away from and back to the game client (via `Alt + Tab`), the world map movement functionality intermittently freezes. 

Clicks issued on the map interface fail to register or update character navigation, forcing the player to close the map overlay, issue a manual movement command using standard character controls (WASD/click), and then reopen the map to restore point-and-click navigation.

---

## Steps to Reproduce
1. Open the game client and open the world map.
2. Click on the map to issue a character movement command.
3. Rapidly or repeatedly switch window focus by pressing `Alt + Tab` back and forth between the game and other desktop applications.
4. Return focus to the game and attempt to click a new destination on the active map screen.
5. Observe that map clicks no longer register or trigger character movement.
6. Close the map, move the character manually via primary movement controls, reopen the map, and observe that map navigation functions normally again.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | Alt-tabbing out of and back into the client should preserve input focus, allowing map point-and-click movement to function without interruption. |
| **Actual Result** | The map interface stops responding to navigation clicks after window focus toggles, requiring manual movement outside the map UI to reset input handling. |

---

## Technical Observations & Potential Causes
* **Window Focus / Input Listener Loss:** Losing and regaining OS window focus (`OnApplicationFocus(false/true)`) may cause the UI input manager to lose track of pointer down events over map hitboxes without sending a proper reset signal.
* **Navigation Mesh Target Desync:** The client-side movement controller may remain in an unhandled "paused" or "background" input state upon regaining window focus, failing to register new map raycasts until the player character's physical transform is manually updated by direct movement inputs.
