---
id: BUG-021
title: "XP Calculator Automatically Applies Unequipped Gear XP Bonuses"
game: Bitjita
company: Community Tool
category: "UI / XP Calculator & Gear Sync"
severity: Medium
status: Submitted
---

# BUG-021: XP Calculator Automatically Applies Unequipped Gear XP Bonuses

## Problem Description
In the **Bitjita XP Calculator**, the tool automatically detects and applies passive gear XP bonuses to calculation totals for items that are not currently equipped on the player character. 

Specifically, under the **XP BONUS** section, the calculator automatically includes a **+8% bonus** attributed to *"Forgotten Librarian's Book (IV)"* as "equipped gear", even when the item is absent from the character's active equipment slots in-game. This inflates the predicted experience rates and distorts level progression estimates.

---

## Steps to Reproduce
1. Navigate to **Bitjita -> XP Calculator**.
2. Connect or sync character data where *"Forgotten Librarian's Book (IV)"* is owned in inventory/storage but **not equipped**.
3. Inspect the active multiplier list under the **XP BONUS** breakdown section.
4. Observe that the **+8% bonus** from *"Forgotten Librarian's Book (IV)"* is listed under "equipped gear" and factored into net XP calculations.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | The XP Calculator should only include XP bonuses from active equipped gear, active food/consumable buffs, or explicit manual user toggles. |
| **Actual Result** | The calculator automatically parses and applies the +8% gear bonus from unequipped items in inventory/storage, overestimating total XP gains. |

---

## Technical Observations & Potential Causes
* **Inventory vs. Loadout API Query Filter:** The calculation parser may be querying the user's general inventory/storage snapshot instead of filtering strictly for active equip slots (`equipment_loadout`).
* **Cached Gear State Multiplier:** The calculator logic may be matching item IDs against an internal passive bonus table without evaluating the boolean `is_equipped` state tag returned by the game's data sync.
