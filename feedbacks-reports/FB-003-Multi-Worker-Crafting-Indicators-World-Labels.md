---
id: FB-003
title: "Multi-Worker Indicators and World Label Visualization for Crafting Stations"
game: BitCraft Online
company: Clockwork Labs
category: "UI / Crafting & World Labels"
status: Submitted
---

# FB-003: Multi-Worker Indicators and World Label Visualization for Crafting Stations

## Problem Description
Currently, there is no direct feedback showing how many players are actively contributing to an ongoing crafting job at a station without manually monitoring the incremental progress bar. This forces players to guess or perform redundant labor to verify if someone else is already assisting with a craft.

Additionally, world labels for crafting stations only display generic information (`"X Crafting"`), making it impossible to see at a glance what specific tiers or types of crafting jobs need assistance without opening each station individually.

---

## Proposed Solution
Enhance both the **Crafting Station UI** and **World Labels** to provide real-time visibility into active workers and pending jobs:

1. **Active Worker Count:**
   * **In Crafting UI:** Display an active contributor count on the job panel (e.g., *"3 Players Working on this Project"*).
   * **In World Labels:** Append an active worker indicator to floating station labels (e.g., `"2 Crafting (👥 3 Active Workers)"`).

2. **Expanded World Label Job Breakdown:**
   * Display available job counts and item tiers directly on the floating world label (e.g., `"3 Jobs Available: [T3 Refined Timber]"`).
   * Implement a threshold overflow for stations with extensive queues (e.g., showing the top 2 priority jobs followed by `"+4 more jobs"`).

---

## User Experience & Value
* **Prevents Redundant Labor:** Crafters can instantly identify which stations already have sufficient workers assigned and redirect their efforts elsewhere.
* **Improves Cooperative Workflow:** Clearer job availability labels allow players to quickly scan settlements for stations that need craft assistance without opening every station interface.
* **Enhanced Settlement Awareness:** Gives settlements and guilds a better real-time overview of active production bottlenecks across their territory.
