---
id: BUG-018
title: "Mortgage Financing Modal Extends Beyond Screen Bounds, Trapping Player Without Confirm/Cancel Buttons or ESC Key Functionality"
game: GG Life
company: AfterGlow Games
category: "UI / Modal Anchoring & Layout Scaling"
severity: High
status: Submitted
---

# BUG-018: Mortgage Financing Modal Extends Beyond Screen Bounds, Trapping Player Without Confirm/Cancel Buttons or ESC Key Functionality

## Problem Description
When opening the real estate financing interface for a property with multiple mortgage options, the modal dialog height exceeds the screen viewport boundaries. 

Because the modal is vertically clipped, the action control buttons (Confirm, Cancel, or Close) at the bottom of the window are rendered entirely off-screen. Furthermore, the UI modal fails to catch the `Escape` key input to dismiss the window, soft-locking the player in the menu and forcing a hard application restart to resume play.

---

## Steps to Reproduce
1. Navigate to the **Assets** or real estate purchase menu in *GG Life*.
2. Select a property and choose the option to finance via mortgage.
3. Select any of the available mortgage types (e.g., *10-Year Fixed Mortgage*).
4. Observe that the modal modal height scales vertically past the bottom edge of the display, cutting off action buttons.
5. Press the `Escape` key or click outside the modal boundaries.
6. Observe that the interface does not close or submit, trapping the player in the financing screen.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | The financing modal should fit dynamically within the screen viewport (or support vertical scrolling) with visible Confirm/Cancel buttons, and pressing `Escape` should close the window. |
| **Actual Result** | The modal extends off-screen, clipping action buttons out of view, while keybindings (`Escape`) fail to dismiss the modal, creating a progression-blocking soft-lock. |

---

## Technical Observations & Potential Causes
* **Fixed Vertical Offset / Lack of Responsive Scaling:** The modal container appears to use fixed pixel offsets or unconstrained content stacking (listing 5 distinct mortgage types), pushing the container footer off-screen on certain aspect ratios/resolutions without enabling an internal `ScrollView` wrapper.
* **Missing Input Map Anchor for Cancel Action:** The modal UI panel lacks an active keypress listener for the `Escape` action cancel event, preventing fallback menu dismissal when UI components are unreachable.
