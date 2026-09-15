---
id: BUG-020
title: "Compendium Tooltip Typo Displays Maximum Stamina Debuff as 0 for Reckless Mushrooms"
game: BitCraft Online
company: Clockwork Labs
category: "UI / Tooltips & Localization"
severity: Low
status: Submitted
---

# BUG-020: Compendium Tooltip Typo Displays Maximum Stamina Debuff as 0 for Reckless Mushrooms

## Problem Description
In the Compendium interface, inspecting any Reckless Mushroom variant (e.g., *Simple Reckless Mushroom*) displays an incorrect value under its poison effect sub-header. 

The Compendium tooltip displays **Maximum Stamina: 0**, missing both the negative sign and the percentage scalar. However, the actual active game state debuff (visible under active status effects when consumed) correctly applies a **Maximum Stamina -60%** modifier.

---

## Steps to Reproduce
1. Open the **Compendium** menu in-game.
2. Search for and select a Reckless Mushroom item (e.g., *Simple Reckless Mushroom*).
3. Inspect the sub-tooltip details under the **Reckless Poison** effect header.
4. Observe that the stat line displays **Maximum Stamina: 0** instead of **-60%**.
5. Consume the mushroom to trigger the active debuff and observe that the active status icon correctly displays **Maximum Stamina -60%**.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | The Compendium tooltip should display **Maximum Stamina -60%** (or the corresponding tier percentage) to match the active debuff effect. |
| **Actual Result** | The Compendium UI displays **Maximum Stamina 0**, misleading players about the penalty mechanics. |

---

## Technical Observations & Potential Causes
* **String Formatting / Parsing Error:** The UI string renderer for the Compendium item data source may be truncating the percentage float or failing to map the dynamic debuff modifier variable, defaulting to `0` instead of parsing `-60%`.
* **Static Asset Data Mismatch:** The static tooltip string definition inside the Compendium database is hardcoded incorrectly relative to the active status effect table.
