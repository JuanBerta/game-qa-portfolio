---
id: BUG-016
title: "Tree Hiding Proximity Threshold and Dynamic Occlusion Malfunction Over Time"
game: BitCraft Online
company: Clockwork Labs
category: "Graphics / Foliage Rendering & Keybinds"
severity: Medium
status: Submitted
---

# BUG-016: Tree Hiding Proximity Threshold and Dynamic Occlusion Malfunction Over Time

## Problem Description
The toggleable "Hide Nearby Trees" function (default keybind `X`) exhibits a gradual rendering degradation over extended play sessions. 

Initially, toggling tree hiding removes surrounding foliage within a generous proximity radius (retaining only harvestable stumps). Over time, the required distance to trigger tree occlusion shrinks significantly. Eventually, the dynamic hiding feature stops functioning automatically, requiring players to double-toggle the `X` key to manually refresh foliage occlusion states.

---

## Steps to Reproduce
1. Press the `X` key to activate the "Hide Nearby Trees" feature.
2. Play the game continuously for an extended session while navigating areas with dense foliage.
3. Observe that after a period of time, the proximity radius for hiding trees shrinks, requiring the player character to stand significantly closer to trees to trigger transparency/occlusion.
4. Continue playing and observe that foliage occlusion stops updating automatically altogether.
5. Press the `X` key twice (toggle off and on) to manually force the tree hiding pipeline to refresh.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | The tree-hiding feature should maintain a consistent activation radius and automatically hide nearby foliage indefinitely while active. |
| **Actual Result** | The activation radius degrades over time until dynamic hiding completely halts, requiring manual key toggles to reset the rendering state. |

---

## Technical Observations & Potential Causes
* **Distance/Spatial Indexing Cache Leak:** The spatial partitioning or distance-check cache for dynamic foliage occlusion may suffer from a memory leak or stale node index accumulation, reducing the effective radius calculation.
* **Occlusion Event Listener Failure:** The tick listener evaluating player proximity relative to foliage colliders may unregister or lose priority in the render pipeline during long sessions, preventing automatic UI/graphics updates.
