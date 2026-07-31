---
id: BUG-013
title: "XP Calculator Target Level Input Intermittently Resets to Maximum (120)"
game: BitCraft Online
tool: Bitjita (Third-Party)
category: "XP Calculator / Input Handling"
severity: Low
status: Submitted
---

# BUG-013: XP Calculator Target Level Input Intermittently Resets to Maximum (120)

## Problem Description
In the Bitjita **XP Calculator**, manually modifying the **"Target"** level input field occasionally causes the value to automatically snap back to the maximum cap (120). 

This occurs during text selection editing (e.g., highlighting the existing number with the mouse to overwrite it) or single-character modifications, forcing the user to re-enter their desired target level.

---

## Steps to Reproduce
1. Navigate to **Bitjita -> XP Calculator**.
2. Select any profession/skill from the list.
3. Focus the **Target** level input field and attempt to modify the value (either by dragging to highlight/select all text, or by backspacing/editing character by character).
4. Observe that the input value unexpectedly resets to `120`, overriding the user's manual entry.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | The Target level field should allow smooth text selection and editing, updating dynamically to the user's specified integer without premature resets. |
| **Actual Result** | The input value intermittently defaults back to the maximum value of 120 during manual text highlight or character editing. |

---

## Technical Observations & Potential Causes
* **Aggressive OnBlur / OnChange Validation:** The input change listener or blur handler may be evaluating transient invalid states (such as an empty string `""` during text highlights/backspaces) and immediately defaulting the fallback state to `120` instead of waiting for input completion.
* **Controlled Component Re-render Race:** If using state-driven UI frameworks (React/Vue), rapid text selection or value replacement may trigger a state update cycle that falls back to `maxVal` (120) before the new keystroke or paste event registers in state.
