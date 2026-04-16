# Loot, Muling, And Shared Features

ScriptForge includes shared framework features so each visual script does not need to rebuild common script behavior.

For a complete plain-English list of what is enabled, disabled, or automatic by default, read [Default Behaviours](default-behaviours.md).

## Loot Tab

The `Loot` tab defines what the shared economy features care about.

It has three sections:

- `Sell`: items that should be sold.
- `Mule`: items that should be given to the mule.
- `Uniques`: valuable drops that should be treated as unique items.

For sell and mule items:

- `Name`: item name.
- `Keep threshold`: how many to keep before selling or muling extras.
- `Withdraw noted`: whether the item should be withdrawn noted when possible.

Unique items are defined by the script, not by the mule config.

The Loot tab does not make items sell or mule by itself. It is the list used by blocks and shared framework tasks when selling, muling, or unique handling is triggered.

## Sell Loot

The `Sell loot` block triggers the shared selling flow.

It uses the `Sell` list from the Loot tab.

Typical use:

```text
If inventory is full
  Sell loot
```

You can also let muling trigger sell first when the framework mule flow needs it.

## Prepare Mule

The `Prepare mule` block triggers the shared sell-then-mule flow.

It uses:

- The `Sell` list.
- The `Mule` list.
- The `Uniques` list.
- The `Muling` config.

Typical use:

```text
Prepare mule
```

Or behind a condition:

```text
If inventory contains item id ItemId.AIR_ORB
  Prepare mule
```

## Muling Config

The script config has a `Muling` section.

Important fields:

- `Mule enabled`: turns muling on.
- `Mule key`: key or identifier used by your mule setup.
- `Coins to receive`: how many coins the script should request when reverse-muling. If empty while muling is enabled, the default is `5000000`.
- `Trigger on timer`: allows timed muling.
- `Timer hours`: how often timed muling should happen. If empty while timer trigger is enabled, the default is `4`.

Default behavior:

- If `Mule enabled` is off, muling does nothing.
- If `Mule enabled` is on, unique-item muling is on by default.
- Unique-item muling uses the `Uniques` list from the Loot tab.
- Timer muling only happens when `Trigger on timer` is enabled.
- If timer muling is enabled and `Timer hours` is empty or invalid, the default is `4` hours.
- If reverse-muling needs coins and `Coins to receive` is empty or invalid, the default is `5000000` coins.

## Webhook Config

The script config has a `Webhook` section.

Important fields:

- `Webhook URL`: destination URL. If this is empty, webhooks are disabled.
- `Post on script stop`: sends a message when the script stops.
- `Post on ban`: sends a message when the account is banned or disabled.
- `Post unique items`: sends a message when unique items are detected.

## Misc Config

The script config has a `Misc` section.

Important fields:

- `World hop profile`: controls which worlds the world-hop blocks prefer.
- `Using poor proxy`: tells shared logic to be more conservative where supported.
- `Renew membership`: allows the shared membership renewal task to redeem or buy bonds when membership credit is low.

World hop blocks such as `Hop random world`, `Hop next world`, and `Hop previous world` use the configured world hop profile.

Default behavior:

- If `World hop profile` is empty, ScriptForge uses a default profile that allows all world locations.
- `Using poor proxy` is off by default.
- `Renew membership` is off by default. Membership renewal will not run unless you enable it.

## Shared Tasks Running In The Background

ScriptForge includes several shared tasks:

- Config handling.
- Restock handling when loadout items have restock data.
- Selling when a sell intent is triggered.
- Muling when `Mule enabled` is on and a mule intent is triggered.
- Audio handling.
- Membership renewal when `Renew membership` is enabled.
- Toggle run by default around `20` to `30` run energy.
- Death handling for normal Death's Domain recovery.
- Stop handling with reason logging and optional stop webhook.

You do not normally add these yourself. They are part of the ScriptForge script.

## Death Handling

Death handling is shared.

It is intended for normal Death's Domain recovery behavior. It does not replace special method-specific item retrieval logic.

If a death fee cannot be paid, shared state can request reverse-muling coins so the script can recover.

If muling is disabled and Death's fee cannot be paid, ScriptForge stops with a reason.

## Restocking Defaults

Restocking is tied to loadouts.

If a missing loadout item has restock data, the shared bank/restock behavior can submit a Grand Exchange buy offer for it.

Default restock behavior:

- Buy retries wait at least `30` ticks.
- Buy retry prices are increased to about `110%`.
- Sell retry prices are reduced to about `90%`.
- Retry prices avoid going beyond about `150%` of the known high price.
- Bonds are collected as items when possible.
- Sold stackable items are collected as items when possible.
- Sold non-stackable items are collected as notes when possible.
- Otherwise, collected items go to the bank.

Ironmen stop if a restockable item is missing, because they cannot restock through the Grand Exchange.

## Runtime And Skill Paint

ScriptForge shows runtime and skill paint information through the shared paint system.

The exact display depends on the client paint view, but the script exposes:

- Runtime.
- Skill information.
