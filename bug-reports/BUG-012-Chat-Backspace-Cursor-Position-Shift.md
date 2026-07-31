---
id: BUG-012
title: "Chat Input Cursor Position Shifts Backward When Rapidly Pressing Backspace"
game: BitCraft Online
company: Clockwork Labs
category: "UI / Chat Input & Text Editing"
severity: Low
status: Submitted
---

# BUG-012: Chat Input Cursor Position Shifts Backward When Rapidly Pressing Backspace

## Problem Description
When editing or deleting long text strings within the chat window, repeatedly pressing the `Backspace` key intermittently causes the text caret (cursor position) to jump backward to a previous character instead of remaining at the active deletion point. 

This caret desync forces players to manually navigate back to the end of the text string (or click the forward position) to resume deleting or editing text accurately.

---

## Steps to Reproduce
1. Open the in-game chat window and enter a long string of text.
2. Press and hold or repeatedly hit the `Backspace` key to delete characters sequentially.
3. Observe that after several deletions, the cursor position unexpectedly shifts left/backward into the preceding text.
4. Note that subsequent character deletions or keypresses occur at the incorrect mid-text cursor position rather than the end of the line.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | Pressing `Backspace` should consistently remove the character immediately preceding the caret while maintaining smooth, predictable cursor placement. |
| **Actual Result** | The caret desynchronizes during repeated deletions, jumping backward into prior characters within the text buffer. |

---

## Technical Observations & Potential Causes
* **Text Mesh / Caret Calculation Race Condition:** Rapid backspace key events may update the internal string index faster than the UI text caret position logic updates, resulting in an index mismatch during dynamic string re-indexing.
* **UTF-8 / Multi-byte Input Handling:** The input parser may be miscalculating character boundary offsets during rapid deletion sweeps, causing the cursor index calculation to step back an extra character position.
