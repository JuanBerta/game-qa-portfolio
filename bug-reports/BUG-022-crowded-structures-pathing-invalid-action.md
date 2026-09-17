---
id: BUG-022
title: "Crowded Structures Cause Player Pathing to Abort with 'Invalid Action' Error"
game: BitCraft Online
company: Clockwork Labs
category: "Gameplay / Pathfinding & Collision"
severity: Medium
status: Submitted
---

# BUG-022: Crowded Structures Cause Player Pathing to Abort with 'Invalid Action' Error

## Problem Description
When navigating through high-density environments—such as active player settlements packed with crafting stations and structures—character pathfinding frequently fails mid-route. 

Initiating long-distance movement through congested areas causes the player character to halt abruptly before reaching the intended target, triggering an **"Invalid Action"** error popup on screen.

---

## Steps to Reproduce
1. Travel to a densely populated player settlement containing multiple adjacent crafting stations or buildings.
2. Click on a destination on the opposite side of the settlement to initiate long-range automated pathfinding.
3. Observe the character's movement as they navigate near adjacent structure collision boxes.
4. Note that movement halts mid-route and an **"Invalid Action"** toast notification appears.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | The player character smoothly navigates around all structure collision boundaries and completes the path to the selected target. |
| **Actual Result** | Pathing aborts unexpectedly mid-route, character movement stops, and the system displays an **"Invalid Action"** error message. |

---

## Technical Observations & Potential Causes
* **NavMesh / Node Recalculation Failure:** Complex overlapping collision boundaries in tight player settlements may cause the pathfinding algorithm to hit an invalid or obstructed node, causing the server validation check to reject the movement vector and return an `Invalid Action` response.
* **Client-Server Desync:** Minor discrepancy between the client-predicted pathing route and the server-side collision validation in dense object clusters causes the server to cancel the action.
