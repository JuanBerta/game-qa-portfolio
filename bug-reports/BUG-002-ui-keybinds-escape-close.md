---
id: BUG-002
title: "Keybinds Settings Window Cannot Be Closed with Escape Key"
game: BitCraft Online
company: Clockwork Labs
category: "UI/UX / Accessibility & Controls"
severity: Low
status: Submitted
---

# BUG-002: Keybinds Settings Window Cannot Be Closed with "Escape" Key

## Problem Description
When navigating the settings menu, the "Keybinds" section does not respond to the `Escape` (`Esc`) key. Unlike other menu windows in the game, the player is unable to close this screen using keyboard input and is forced to manually click the close button with the mouse.

---

## Steps to Reproduce
1. Open the **Settings** menu.
2. Navigate to and click on the **Keybinds** section.
3. Press the `Esc` key on the keyboard.
4. Observe that the settings window does not close.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | Pressing the `Esc` key closes the Keybinds window and returns the player to the game/previous screen, consistent with standard UI behavior. |
| **Actual Result** | The `Esc` keypress is completely ignored, forcing the player to manually click the "Close" button with the mouse. |

---

## Technical Observations & Potential Causes
* **Input Listener Consumption:** The Keybinds remapping listener may be capturing or suppressing global keypress events (including `Esc`) to prevent accidental menu closure while assigning keys, without falling back to menu navigation when remapping is inactive.
* **UI Focus State:** The window focus state may fail to register standard cancel commands (`Cancel` / `UI_Back`) when the sub-panel is opened.
