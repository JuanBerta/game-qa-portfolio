---
id: FB-019
title: "Auto-Resume Gathering/Crafting After Stamina Recovery and Auto-Eat Food When Effects Expire"
game: BitCraft Online
company: Clockwork Labs
category: "Feedback / Quality of Life & Stamina Management"
severity: Feature Request / QoL
status: Submitted
---

# FB-019: Auto-Resume Gathering/Crafting After Stamina Recovery and Auto-Eat Food When Effects Expire

## Problem Description
During long gathering or crafting sessions, the player has to keep manually monitoring two things:

1. **Stamina:** When stamina runs out, the active gathering or crafting action stops. Once stamina has recovered, the player must notice this and manually start the activity again.
2. **Food effects:** When a food buff expires, the player must notice it and manually eat another food item from the inventory to keep the benefit active.

Both tasks interrupt sustained play and are easy to miss, which costs time and progress, especially during long, AFK-style sessions.

---

## Feedback & Proposed Solutions

### Solution 1: Auto-Resume Activity After Full Stamina Recovery (Checkbox)
* **Option:** Add a checkbox (e.g., *"Auto-resume activity after stamina recovers"*) in the settings or on the active activity UI.
* **Behavior:** When enabled, if the player runs out of stamina while gathering or crafting and later recovers their **full** stamina, the same activity starts again automatically (same recipe or resource target, same station or node context).
* **Suggested safeguard:** Automatic restart should not trigger if the player manually stopped the activity, moved away from the station or node, or changed the activity target.

### Solution 2: Auto-Eat Food When Effect Expires (Checkbox)
* **Option:** Add a checkbox (e.g., *"Auto-eat food when effect ends"*) in the settings or on the food/effects UI.
* **Behavior:** When enabled, once a food effect stops, the game automatically consumes a food item from the player's inventory to reapply the effect.
* **Suggested safeguard:** If the inventory has no suitable food, the feature should do nothing and notify the player, and it should never consume food the player has marked as protected or reserved.

---

## Expected Impact
* Reduces manual interruptions during long gathering and crafting sessions.
* Lets players keep progress going while stamina recovers, without constant monitoring.
* Keeps food buffs active consistently, which supports stamina and efficiency management during sustained activity.
* Both options are opt-in checkboxes, so players who prefer full manual control are unaffected.
