---
id: FB-002
title: "Market Improvements: Supporting High-Volume Trade & Fractional Pricing"
game: "BitCraft Online"
company: "Clockwork Labs"
category: "Feature Proposal / Economy & UI Friction"
status: "Submitted"
---

# FB-002: Market Improvements — Supporting High-Volume Trade & Fractional Pricing

## Overview
Currently, the minimum listing price for any item on the global Market is fixed at **1 Hex Coin per item**. For low-tier, high-volume items (such as raw materials, basic ores, or refined logs), this floor creates a significant price distortion.

Because of this 1-coin minimum, players trading in bulk are forced to bypass the global Market entirely and rely on personal **Trader Stands** to offer fractional pricing (e.g., offering large bundles of items for a single flat coin amount).

To unify the economy and give players a smoother trading experience, I propose updating the global Market to support either **decimal/fractional pricing** or **custom bulk-bundle orders**.

---

## The Current Friction

* **Market Disconnect:** When high-volume materials are artificially pegged to a minimum of 1 Hex Coin each, their market price often doesn't match their actual value relative to lower-volume, high-tier goods.
* **Over-reliance on Trader Stands for Basic Supplies:** Players who want to sell bulk items at true market value must physically set up and manage Trader Stands to offer bundle ratios (e.g., 20 items for 1 Hex Coin).
* **Loss of Liquidity:** Traders who prefer using the global Market are disincentivized from listing bulk supplies, leading to reduced liquidity for basic crafting components across settlements.

---

## Proposed Solutions

### Option A: Support Decimal Pricing on the Market
Allow players to set unit prices as decimals below 1 Hex Coin (e.g., **0.05 Hex Coins per unit**).

* **Calculation:** When a buyer purchases a stack, the total cost rounds up or down to the nearest full Hex Coin (or uses a minimum purchase threshold so transactions always equal at least 1 Hex Coin).
* **Benefit:** Straightforward UI, easy for buyers to compute total cost, and aligns with standard MMO market mechanics.

### Option B: Adopt Trader Stand "Bundle" Orders on the Market
Allow players to create Market listings using the same trade format as Trader Stands: **"Offer X items for Y Hex Coins"** (or item-for-item barter exchanges).

* **Calculation:** The listing treats the bundle as a single unit trade rather than enforcing an individual unit price limit.
* **Benefit:** Reuses existing Trader Stand trade logic while making bulk offers globally searchable and accessible.

---

## Economic & Quality-of-Life Benefits

* **Healthier Commodity Pricing:** High-volume, low-tier goods can naturally find their true supply-and-demand market value without hitting an artificial floor.
* **Centralized Bulk Trade:** Players don't have to wander through dozens of individual Trader Stands just to buy basic crafting supplies in bulk at fair rates.
* **Better Market Scalability:** As the game progresses and high-tier gear inflates in value, lower-tier items can cleanly scale down in unit price without breaking trade loops.
