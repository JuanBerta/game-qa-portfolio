---
id: BUG-010
title: "Player 'Items' Section Fails to Display Item and Cargo Storage Inventory"
game: BitCraft Online
tool: Bitjita (Third-Party)
category: "Player Profile / Inventory & Cargo Storage"
severity: Medium
status: Submitted
---

# BUG-010: Player 'Items' Section Fails to Display Item and Cargo Storage Inventory

## Problem Description
In the Bitjita Player Search profile, navigating to the **"Items"** tab fails to render items located within a player's **Item Storage** or **Cargo Storage**, even when those storage slots contain active inventories in-game.

The interface omits these storage containers entirely or displays them as empty, preventing users from viewing a comprehensive breakdown of a player's full stored assets.

---

## Steps to Reproduce
1. Open the **Bitjita** website and use the **Player Search** input field.
2. Select a valid player profile that currently has items in their Item or Cargo Storage in-game.
3. Click on the **Items** section/tab within the player profile view.
4. Observe that Item Storage and Cargo Storage sections fail to display or populate with stored items.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | The "Items" section should query and render all stored player inventories, including Item Storage and Cargo Storage containers. |
| **Actual Result** | Item Storage and Cargo Storage contents are absent from the profile view, showing no stored items. |

---

## Technical Observations & Potential Causes
* **Missing API Endpoint/Data Field:** The API request fetching player profile data may be missing parameters or schemas required to pull Item/Cargo storage container data tables from the telemetry backend.
* **UI Parsing/Filtering Logic Error:** The frontend inventory component may be filtering out specific storage container types (e.g., matching on personal inventory IDs while ignoring deployable/cargo storage container IDs).
