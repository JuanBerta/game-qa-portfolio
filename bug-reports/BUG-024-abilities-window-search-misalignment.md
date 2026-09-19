---
id: BUG-024
title: "Filtered Search Results Misaligned in Abilities Window UI"
game: BitCraft Online
company: Clockwork Labs
category: "UI / Layout & Navigation"
severity: Low
status: Submitted
---

# BUG-024: Filtered Search Results Misaligned in Abilities Window UI

## Problem Description
When opening the **Abilities** panel and filtering items using the search bar, the resulting ability cards (such as prospecting abilities) display with incorrect UI alignment and positioning relative to the container grid and sidebar navigation tabs.

---

## Steps to Reproduce
1. Open the **Abilities** menu window in-game.
2. Click on the search input field at the top of the panel.
3. Type the name of an ability (e.g., search `"berser"` for *Berserker Mushroom Hunt*).
4. Observe the horizontal and vertical alignment of the matching result card inside the list view area.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | Search results should render neatly aligned to the top-left margin of the content area with consistent padding and grid structure. |
| **Actual Result** | Filtered ability cards render offset from the expected container margins, breaking UI alignment standards relative to active tab boundaries. |

---

## Technical Observations & Potential Causes
* **Layout Group Anchor / Padding Offset:** Filtering items in the search view may fail to reset the scroll view container padding or grid layout group offset, causing elements to maintain an incorrect baseline coordinate.
* **Dynamic Item Template Spacing:** The search filter UI container may lack proper layout auto-reflow bindings, leading to orphan elements being positioned arbitrarily when hidden siblings are unmounted.

## Screenshot

![Wrong Alignment in Abilities Window Example](/bug-reports-images/BUG-024.png)