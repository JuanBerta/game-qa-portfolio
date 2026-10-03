---
id: BUG-003
title: "Unparsed Rich Text Tags Display in Quest Objective Text"
game: BitCraft Online
company: Clockwork Labs
category: "UI / Formatting & Localization"
severity: Low
status: Submitted
---

# BUG-003: Unparsed Rich Text Tags Display in Quest Objective Text

## Problem Description
In the Quest UI, certain task description strings display raw, unparsed rich-text styling tags (`<style=highlight>` and `</style>`) instead of applying the intended visual text formatting (such as highlighted/colored text).

This issue is visible in the **Fishing IV: A Runaway Lead** quest panel under the **Tasks** section.

---

## Steps to Reproduce
1. Open the Quest/Journal menu.
2. Select the quest **Fishing IV: A Runaway Lead**.
3. Inspect the text under the **Tasks (0/3)** section on the right-hand panel.
4. Observe the raw markup tags rendered directly in the objective descriptions for:
   * `Craft <style=highlight>[Basic Chum]</style>`
   * `Locate a <style=highlight>[School Of Briny Linus]</style>`

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | The target item/location names (e.g., `[Basic Chum]` and `[School Of Briny Linus]`) display with highlighted text formatting, with `<style>` tags stripped/parsed by the UI text renderer. |
| **Actual Result** | The raw markup strings `<style=highlight>` and `</style>` are explicitly rendered as plain text within the UI box. |

---

## Technical Observations & Potential Causes
* **Text Renderer Parsing Error:** The UI text component (e.g., TextMeshPro or custom rich-text parser) may either have rich-text parsing disabled for these specific objective fields or lack the corresponding `highlight` style definition in the UI style sheet.
* **Localization / String Escaping:** The string entry in the localization table may be escaping the `<>` angle brackets or utilizing a style tag that isn't registered in the active theme config.
