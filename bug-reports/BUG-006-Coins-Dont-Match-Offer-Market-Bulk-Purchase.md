---
id: BUG-006
title: "Transaction Failure with 'Coins don't match the offer' Error When Purchasing Multi-Priced Market Listings"
game: BitCraft Online
company: Clockwork Labs
category: "Economy / Market & Trading"
severity: Medium
status: Submitted
---

# BUG-006: Transaction Failure with "Coins don't match the offer" Error When Purchasing Multi-Priced Market Listings

## Problem Description
When attempting to purchase a batch of items from the settlement market that includes multiple listings of the same item at different prices (specifically involving your own listings, or a mix of your items and another player's items at varying prices), the transaction fails entirely. 

Instead of processing the valid selections, the system blocks the purchase and triggers an error message stating **"Coins don't match the offer"**.

---

## Steps to Reproduce
1. Open the settlement market interface.
2. Select or add multiple listings of an item to your purchase cart where the items have different listing prices (e.g., purchasing multiple of your own items listed at two different prices, or a mix of your items and another player's items at varying prices).
3. Attempt to execute the bulk purchase for all selected listings.
4. Observe the error message **"Coins don't match the offer"** display on screen, and note that the transaction is aborted with no items exchanged or coins deducted.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | The market system should correctly calculate the cumulative total across differing price points and process the bulk transaction successfully (or handle self-purchase rules/mixed carts gracefully). |
| **Actual Result** | The transaction is rejected with the "Coins don't match the offer" error message, preventing the multi-item batch purchase from going through. |

---

## Technical Observations & Potential Causes
* **Cart Total Calculation Mismatch:** The client-side cost calculation or server-side validation handler may be evaluating the entire batch against a single unit price or expecting a uniform price point, causing a total coin mismatch when aggregating items with heterogeneous pricing.
* **Self-Transaction Validation Flaw:** The economy backend may be failing to properly isolate or exempt player-owned listings when bundled with other market entries, causing the validation logic to miscalculate the required currency exchange.
