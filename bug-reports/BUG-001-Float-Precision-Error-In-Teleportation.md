---
id: BUG-001
title: "Float Precision Error Prevents Teleportation at Exact Energy Values"
game: BitCraft Online
company: Clockwork Labs
category: "Functional / Mathematics & Precision"
severity: Medium
status: Submitted
---

# BUG-001: Float Precision Error Prevents Teleportation at Exact Energy Values

## Problem Description
The game prevents a player from teleporting if their current Teleportation Energy exactly matches the required energy cost displayed in the UI. 

This occurs because the user interface likely displays a rounded integer value, while the backend evaluates the energy as a floating-point number (`float`). As a result, the actual stored value can be infinitesimally lower than the required threshold (e.g., `71.99999` instead of `72.00000`), causing the check to fail.

---

## Steps to Reproduce
1. Navigate to any Waystone.
2. Accumulate or reduce Teleportation Energy until the UI displays the **exact integer quantity** required for a specific teleportation destination (e.g., current energy reads `72` and the travel cost is `72`).
3. Attempt to initiate the teleportation.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | The player successfully teleports when their displayed energy matches or exceeds the required energy cost. |
| **Actual Result** | The player is unable to teleport, and an error message appears indicating there is insufficient energy. |

---

## Technical Observations
This behavior strongly points to a **floating-point precision error**. 

When the backend evaluates a conditional check like:

```csharp
if (currentEnergy >= travelCost)
{
    // Initiate teleportation
}
