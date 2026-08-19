---
id: BUG-017
title: "Mining Rework Spawns (Geodes/Magnetic Chunks) Generate Inside Adjacent Resource Nodes"
game: BitCraft Online
company: Clockwork Labs
category: "Gameplay / Mining & Spawn Mechanics"
severity: Medium
status: Submitted
---

# BUG-017: Mining Rework Spawns (Geodes/Magnetic Chunks) Generate Inside Adjacent Resource Nodes

## Problem Description
When mining resource nodes, secondary spawns introduced in the mining rework (such as Gem Geodes and Magnetic Rock Chunks across all tiers) occasionally spawn directly inside neighboring resource nodes. 

This overlap occurs most frequently around large, tightly grouped node clusters. The parent node's collision box masks the spawned item, preventing player selection or interaction. Because these spawned objects operate on a despawn timer, players are unable to harvest them before they expire.

---

## Steps to Reproduce
1. Locate a cluster where resource nodes are positioned in close physical proximity to one another.
2. Mine a node capable of triggering secondary spawns (Gem Geodes or Magnetic Rock Chunks).
3. Observe the spawning location of the secondary object.
4. Note that the object occasionally instantiates inside the geometry/hitbox of an adjacent node, clipping beneath its model and blocking interaction until it despawns.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | Secondary mining items should spawn on clear, walkable terrain adjacent to the mined node without clipping into nearby objects. |
| **Actual Result** | Secondary items spawn inside neighboring node collision boxes, rendering them unclickable and causing them to despawn lost. |

---

## Technical Observations & Potential Causes
* **Lack of Raycast/Navmesh Spawn Validation:** The scatter/spawn algorithm for secondary mining items may be picking offset coordinates relative to the mined node without checking for existing node colliders or bounding box overlaps at the target coordinate.
* **Tight Clustering Node Density:** Dense node placements lack a minimum clearance buffer, causing fixed radial offset spawns to land directly inside neighboring bounding boxes.
