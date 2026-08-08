---
id: BUG-015
title: "Combat Abilities Fail and Display 'Invalid Action: Expected: Attack' Error During Combat"
game: BitCraft Online
company: Clockwork Labs
category: "Combat / Ability Validation & State Machine"
severity: High
status: Submitted
---

# BUG-015: Combat Abilities Fail and Display 'Invalid Action: Expected: Attack' Error During Combat

## Problem Description
During active combat with monsters, attempting to execute combat abilities intermittently fails and triggers an on-screen warning: `"Invalid Action: Expected: Attack"`. 

When this state occurs, the player character deals zero damage to the target while continuing to take incoming damage from the monster. Additionally, combat animations stutter/degrade during this window. Because the player cannot deal damage or defend effectively, this state sync failure often results in unavoidable character defeat and subsequent death debuffs.

---

## Steps to Reproduce
1. Engage in combat with any monster in the world using weapons and active combat abilities.
2. Continuously execute abilities and basic attacks over the course of an extended combat session.
3. Observe that the game occasionally rejects ability inputs with the warning message: `"Invalid Action: Expected: Attack"`.
4. Note that during this error state, character ability animations hitch, no damage is dealt to the enemy, but enemy attacks continue to inflict damage on the player.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | Combat abilities should execute smoothly and register valid damage hits against monsters without state mismatch errors. |
| **Actual Result** | Ability inputs are rejected by the server, dealing no damage and leaving the player vulnerable to enemy attacks until defeated or reset. |

---

## Technical Observations & Potential Causes
* **Server-Client Combat State Mismatch:** The client ability queue may attempt to dispatch an ability execution packet while the server combat state machine is still expecting a standard light/heavy attack sequence or awaiting cooldown resolution.
* **Desynchronized Animation/Global Cooldown (GCD):** A race condition between local animation triggers and server validation flags can cause the server to reject incoming action requests as invalid, locking the player out of damage execution while keeping their hurtbox active.
