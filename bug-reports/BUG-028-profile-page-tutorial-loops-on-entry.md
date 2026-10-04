---
id: BUG-028
title: "Profile Page Onboarding Tutorial Prompts Repeatedly on Every Page Load"
game: Feudera
company: Feudera
category: "UI / Onboarding & Tutorial Logic"
severity: Medium
status: Submitted
---

# BUG-028: Profile Page Onboarding Tutorial Prompts Repeatedly on Every Page Load

## Problem Description
Every time a player opens or navigates to the **Profile** page (`Your profile`), the initial onboarding tutorial popup automatically triggers and displays over the interface. 

Closing or completing the tutorial overlay does not save its completion state locally or server-side, causing the prompt to trigger again on every subsequent visit to the page.

---

## Steps to Reproduce
1. Navigate to the **Profile** section in the main UI.
2. Observe the onboarding tutorial overlay ("Your profile") opening automatically.
3. Dismiss or close the tutorial popup using the close `X` button or navigating through the sequence.
4. Navigate away to another page/menu.
5. Return to the **Profile** page.
6. Observe that the tutorial overlay pops up again.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | Once completed or closed, the tutorial completion flag should persist so the overlay does not prompt on subsequent visits. |
| **Actual Result** | The profile tutorial opens every single time the profile view is rendered, regardless of prior dismissal. |

---

## Technical Observations & Potential Causes
* **Tutorial State Persistence Failure:** The boolean flag responsible for tracking whether `profile_tutorial_completed` has been viewed is either failing to write to the database/local storage or is being re-initialized to `false` whenever the profile page component mounts.
* **Missing Completion Gate Check:** The route listener or controller loading the Profile view triggers the tutorial modal unconditionally upon mount without checking the account's tutorial progress flags.
