# Default Behaviours

This page explains what ScriptForge and the shared framework do by default.

Some features are always present in the background. Other features are present but do nothing unless you enable a config option or trigger them with a block.

## Quick Summary

| Feature | Default |
| --- | --- |
| Editor mode | Off unless `Open editor` is enabled. |
| Muling | Off unless `Mule enabled` is enabled. |
| Unique-triggered muling | On automatically when muling is enabled. |
| Timer-triggered muling | Off unless `Trigger on timer` is enabled. |
| Timer mule interval | Defaults to `4` hours if timer muling is enabled and no valid value is set. |
| Reverse-mule coins | Defaults to `5000000` coins if muling is enabled and no valid value is set. |
| Webhooks | Off unless `Webhook URL` is filled in. |
| Membership renewal | Off unless `Renew membership` is enabled. |
| Run toggling | On by default. ScriptForge toggles run when energy reaches a random value from about `20` to `30`. |
| Death handling | On by default for normal Death's Domain recovery. |
| Restocking | Available by default when loadout entries have restock data. |
| Poor proxy behavior | Off unless `Using poor proxy` is enabled. |

## Loot Tab Defaults

The Loot tab contains lists used by shared economy features.

It does not sell or mule by itself.

- `Sell`: items the shared sell flow may withdraw and sell.
- `Mule`: items the shared mule flow may withdraw and give to the mule.
- `Uniques`: item names watched as unique drops.

For sell and mule items:

- `Keep threshold` means how many to keep before treating extras as sellable or muleable.
- `Withdraw noted` controls whether the framework tries to withdraw that item noted.

Unique drops are detected from ground item spawn events. If the spawned item name matches the `Uniques` list, ScriptForge can post a webhook and, if muling is enabled, prepare to mule.

## Muling Defaults

Muling is disabled until `Mule enabled` is checked.

When muling is enabled:

- Unique-triggered muling is enabled automatically.
- The unique trigger uses the `Uniques` list in the Loot tab.
- Reverse-muling requests `Coins to receive`.
- If `Coins to receive` is empty or invalid, it uses `5000000`.

Timer muling is separate:

- Timer muling only works when `Trigger on timer` is checked.
- If `Timer hours` is empty or invalid, it uses `4`.
- The timer is checked while the bank is open.
- When the timer is reached, ScriptForge prepares the sell-then-mule flow.

The mule flow uses the `Mule` list from the Loot tab. It also preserves the configured coin threshold before calculating excess coins to mule.

## Selling Defaults

Selling does not happen randomly.

Selling starts when something sets a sale reason, such as:

- You use the `Sell loot` block.
- You use the `Prepare mule` block.
- Timer muling decides it is time to sell before muling.
- Unique-triggered muling decides it should prepare to mule.
- The framework detects that a Grand Exchange offer cannot be bought because the account is low on coins.

The sell flow uses the `Sell` list from the Loot tab.

If selling is part of a mule preparation, ScriptForge sells first. When the sell flow finishes, it switches into the mule flow.

## Reverse-Muling Defaults

Reverse-muling means asking the mule for coins instead of giving items to the mule.

ScriptForge can request coins when:

- A Grand Exchange purchase cannot be afforded after a sale attempt.
- Death's fee cannot be paid and muling is enabled.

If a bond purchase is involved, the framework may request enough coins for the bond price plus a margin. Otherwise it uses `Coins to receive`, or the default `5000000`.

If muling is disabled and the script cannot recover from low coins, the framework may stop the script instead.

## Loadout Banking And Restocking Defaults

Loadout banking is driven by loadout blocks or framework bank tasks.

The shared bank behavior:

- Withdraws the requested backpack loadout.
- Adds missing worn equipment to the backpack loadout so it can be withdrawn and equipped.
- Adds missing carry equipment too.
- Avoids duplicate entries when the same item appears in multiple loadouts.
- Equips missing worn equipment when banking is not needed but equipment is not worn.

Restocking is available when a missing loadout item has restock data.

Default restock behavior:

- Missing restockable items are submitted as Grand Exchange buy offers.
- Ironmen stop if a restockable item is missing, because they cannot restock through the Grand Exchange.
- Retry pricing waits at least `30` ticks.
- Buy retry prices are increased to about `110%`.
- Sell retry prices are reduced to about `90%`.
- Retries avoid going beyond about `150%` of the known high price.

Default collection behavior:

- Bonds are collected as items when there is backpack space.
- Sold stackable items are collected as items when there is backpack space.
- Sold non-stackable items are collected as notes when there is backpack space.
- Otherwise, collections go to the bank.

Wilderness scripts use a wilderness-aware Grand Exchange walk setup so the restock task can leave wilderness behavior cleanly before walking.

## Death Handling Defaults

Death handling is enabled by default.

It is for normal Death's Domain recovery:

- If a gravestone is active, ScriptForge walks to the closest Death's Domain entrance it knows about.
- It enters Death's Domain.
- It talks through Death's reclaim dialog.
- It pays Death's fee when possible.
- It leaves through the portal when finished.

If the fee cannot be paid:

- If muling is enabled, ScriptForge leaves Death's Domain and requests reverse-mule coins.
- If muling is disabled, ScriptForge stops with a reason.

Death handling does not cover special method-specific recovery. For example, if a minigame or boss has its own special item retrieval NPC, that needs script-specific logic.

## Membership Defaults

Membership renewal is off by default.

It only runs when `Renew membership` is checked in Misc config.

When enabled, the renewal task can:

- Hop to a members world when the account has membership credit but is currently on a free world.
- Redeem a bond from the backpack.
- Withdraw a bond from the bank.
- Buy a bond through the Grand Exchange when needed.
- Log out after successfully bonding.

The default renewal policy only allows renewal from common Edgeville and Varrock regions. This avoids trying to renew from random unsafe or inconvenient places.

## World And Login Defaults

If `World hop profile` is empty, ScriptForge creates a default profile that allows all world locations.

World hop blocks use the configured world hop profile:

- `Hop random world`
- `Hop next world`
- `Hop previous world`

Login responses are configured so members-only and membership-required responses are handled by the framework instead of immediately killing the script:

- Members-only area response tries to hop to a members world.
- Membership-required response tries to hop to a free world.

## Webhook Defaults

Webhooks are disabled unless `Webhook URL` is filled in.

When a URL is set, these toggles control what gets posted:

- `Post on script stop`
- `Post on ban`
- `Post unique items`

Stop webhooks include the stop reason.

Unique webhooks use the `Uniques` list from the Loot tab.

## Stop Handling Defaults

The shared stop state can stop the script with a reason.

When a stop is requested:

- The reason is logged.
- A stop webhook is posted if webhooks are configured for script stops.
- The `Stopping` task becomes active and blocks other work.

## Run Toggle Defaults

Run toggling is enabled by default.

ScriptForge turns run on when:

- Run is currently off.
- Energy reaches a random threshold from about `20` to `30`.

Individual scripts can override the run-toggle condition, but ScriptForge uses the default behavior.

## Poor Proxy Defaults

`Using poor proxy` is off by default.

When enabled, some shared bank/sell/mule/restock actions add small sleeps after withdrawals. This is meant to make sensitive or unstable connections less spammy.

