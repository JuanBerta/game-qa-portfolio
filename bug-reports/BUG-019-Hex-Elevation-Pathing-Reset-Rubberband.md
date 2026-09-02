---
id: BUG-019
title: "Movement Pathing Resets Position When Traversing Hexes with Elevation Differences"
game: BitCraft Online
company: Clockwork Labs
category: "Gameplay / Pathing & Elevation Collision"
severity: Medium
status: Submitted
---

# BUG-019: Movement Pathing Resets Position When Traversing Hexes with Elevation Differences

## Problem Description
When navigating across adjacent map hexes that feature varying height limits/elevation changes, the player character (or mounted deployable) occasionally rubberbands or resets back to the previous hex. 

This issue occurs during both manual traversal and automated pathfinding (e.g., clicking on the world map). The pathing/collision validation algorithm appears to miscalculate valid elevation transitions between neighboring hex tiles, temporarily flagging valid terrain height differences as impassable and snapping the player back to their former tile position.

---

## Steps to Reproduce
1. Move a character (on foot or mounted on a deployable) toward a border between two or more hexes that feature noticeable elevation/height differences.
2. Cross the hex boundary using direct movement or map-based pathfinding.
3. Observe that upon entering the new hex, the character stutters and snaps/resets back to the starting hex.
4. Attempt to re-traverse the same path to observe repeated pathing resets at the height threshold.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | Character and mount pathfinding should smoothly transition across valid elevation changes between neighboring hexes. |
| **Actual Result** | The client/server pathing validation detects the height step as out-of-bounds, resetting the character back to the previous hex tile. |

---

## Technical Observations & Potential Causes
* **Height Limit Tolerance Misconfiguration:** The elevation step check between adjacent hex tile meshes may have a tighter tolerance threshold than the actual terrain generation height delta, triggering false-positive impassable terrain flags.
* **Server-Client Movement Reconciliation Sync:** The client-side movement controller predicts valid slope traversal, but the server movement validation calculates a height discrepancy exceeding the mount's maximum step-up limit, forcing a position rollback (rubberbanding).
