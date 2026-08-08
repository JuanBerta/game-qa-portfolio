---
id: FB-006
title: "Add Direct Animal Hunting Actions to XP Calculator"
game: BitCraft Online
tool: Bitjita (Third-Party)
category: "XP Calculator / Hunting Skill"
status: Submitted
---

# FB-006: Add Direct Animal Hunting Actions to XP Calculator

## Problem Description
Currently, the **Hunting** tab in Bitjita's **XP Calculator** only lists carcass refining/carving activities. It omits the actual combat/hunting phase (killing animals in the world) where players earn direct Hunting XP per point of damage dealt to animal health pools.

For example, a *Sagi Bird* grants `2.7 Hunting XP per HP` with a total health pool of `100 HP`, awarding `270 base XP` upon defeat (before tool multipliers or XP buffs). Because combat damage varies based on equipped bow power and RNG variance, direct creature hunting entries are currently missing from the calculator.

---

## Proposed Solution
Add world creature hunting entries to the **Hunting** category in the XP Calculator based on creature total HP and XP-per-HP conversion rates:

1. **Creature Hunting Entries:** List each huntable creature tier/species as an activity line (e.g., *Hunting: Sagi Bird*).
2. **Max HP & Base XP Calculation:** Base the activity's total XP on `Creature Max HP × XP per HP`.
3. **Tool Power / Effort Integration:** Utilize the existing **Tool Power** input system or an estimated hits-to-kill metric to calculate `Actions` / `Time` estimates for hunting batches, accounting for damage variability.

---

## User Experience & Value
* **Comprehensive Skill Tracking:** Gives players a complete view of Hunting leveling paths (combining field combat with carcass processing).
* **Accurate Mob Estimates:** Allows players to calculate exactly how many creatures of a specific tier they need to hunt to reach their target Hunting level.
