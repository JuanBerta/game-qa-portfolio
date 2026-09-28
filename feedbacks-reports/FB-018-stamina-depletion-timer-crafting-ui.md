---
id: FB-018
title: "Displaying Maximum Crafting/Gathering Duration Based on Remaining Stamina"
game: BitCraft Online
company: Clockwork Labs
category: "Feedback / UI & Quality of Life"
severity: Feature Request / QoL
status: Submitted
---

# FB-018: Displaying Maximum Crafting/Gathering Duration Based on Remaining Stamina

## Problem Description
Players currently lack an immediate visual indicator showing how long they can perform an active crafting or gathering action before running out of stamina. 

Determining remaining active time requires manual mental math based on current stamina, stamina cost per action, and time per tick/action cycle (e.g., cross-referencing $1.18\text{s}$ action time against total current stamina). Doing this calculation repeatedly during long crafting or harvesting sessions is tedious and impractical.

---

## Feedback & Proposed Solutions

### Solution: Dynamic Stamina Depletion Timer
* **HUD Progress Bar Label:** Next to the action interval timer (e.g., `1.18s`) on the active HUD progress bar, add a dynamic label displaying the estimated time remaining until current stamina is depleted (e.g., `Stamina left: 3m 45s`).
* **Station Interface Detail:** Include a matching indicator within the Station Crafting Recipe menu directly under the **Estimated time** stat line to show total craftable time relative to current player stamina pool.

---

## Expected Impact
* Provides immediate Quality of Life (QoL) clarity for resource management without requiring manual calculations.
* Helps players time food consumption and stamina recovery cycles more efficiently during sustained crafting/gathering operations.
