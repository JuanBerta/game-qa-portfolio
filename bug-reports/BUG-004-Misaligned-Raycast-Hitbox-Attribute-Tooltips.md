---
id: BUG-004
title: "Misaligned / Narrow Raycast Hitbox for Attribute Breakdown Tooltips"
game: BitCraft Online
company: Clockwork Labs
category: "UI / UX"
severity: Low
status: Fixed
---

# BUG-004: Misaligned / Narrow Raycast Hitbox for Attribute Breakdown Tooltips

## Problem Description
In the Character Detailed Stats menu, hovering over an attribute row to view the tooltip breakdown (showing equipment bonus origins) suffers from inconsistent raycast detection. 

The hover hitbox for triggering the breakdown tooltip does not cover the full attribute entry line. Instead, it only activates when the cursor is placed in specific offset areas—namely slightly to the left of the attribute number or on the far-left edge of the UI row—making the tooltip difficult to trigger naturally during standard navigation.

---

## Steps to Reproduce
1. Open the Character sheet and navigate to the **Detailed Stats** screen.
2. Move the cursor over an attribute row in the list (e.g., `Evasion` under COMBAT).
3. Hover directly over the attribute name or the center of the row; observe that the breakdown tooltip fails to trigger.
4. Shift the cursor slightly to the left of the numeric value (or to the far left of the row entry).
5. Observe that the tooltip pop-up (e.g., Evasion breakdown showing gear contributions) finally appears.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | Hovering anywhere over the bounding box of a stat row (including the icon, text label, and numerical value) should reliably trigger the attribute breakdown tooltip. |
| **Actual Result** | The interactive hover region is misaligned or undersized, requiring precision hovering slightly to the left of the numerical stat value or on the far-left margin of the row. |

---

## Technical Observations & Potential Causes
* **Raycast Bounds Misalignment:** The `Raycast Target` bounds (e.g., `Image` component or `RectTransform` area acting as the tooltip trigger) do not match the full visual container of the stat row entry, creating large dead zones across the label and number elements.
* **Child Element Raycast Interference:** Underlying text components or child UI elements within the stat row may have `Raycast Target` enabled without proper event pass-through, blocking or intercepting hover events intended for the parent tooltip trigger container.
