---
id: FB-004
title: "Sort Crafting Station Recipes by Resource Input Tier"
game: BitCraft Online
company: Clockwork Labs
category: "UI / Crafting & Station Menus"
status: Submitted
---

# FB-004: Sort Crafting Station Recipes by Resource Input Tier

## Problem Description
Currently, items with multiple alternative recipes using similar inputs across different tiers (e.g., crafting an **"Empty Bucket"** using Tier 1 through Tier 10 Planks) are listed in an inconsistent or unsorted order within station menus. 

Because recipes are not organized sequentially by input tier, players are forced to manually scan through every variation in the recipe list to locate the specific craft matching their available inventory tiers.

---

## Proposed Solution
Implement a systematic ascending tier sort (T1 through T10) for all recipes that produce the same output item using variable-tier inputs:

1. **Sequential Tier Ordering:** Automatically sort recipe entries in crafting station interfaces strictly by the tier of the primary ingredient (e.g., *T1 Wood -> T2 Wood -> T3 Wood...*).
2. **Visual Tier Grouping:** Maintain consistent vertical positioning so higher-tier material crafts consistently appear further down (or grouped logically) within the recipe selection panel.

---

## User Experience & Value
* **Streamlined UI Navigation:** Eliminates visual clutter and speeds up recipe selection when working with multi-tier utility items.
* **Reduced Friction for Crafters:** Players can instantly locate and execute crafts based on the tier of raw or refined materials currently in their inventory without manually hovering over every entry.
