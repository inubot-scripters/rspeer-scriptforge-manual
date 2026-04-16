# Troubleshooting

Start here when the script does something surprising.

## The Editor Does Not Open

Check:

- `Open editor` is enabled.
- `Script file` is filled in.

ScriptForge will not open the editor before a script file is configured.

## The Script Opens The Editor Instead Of Running

Disable `Open editor` in the script config.

When `Open editor` is enabled, ScriptForge is in edit mode. It opens the editor and does not run the block tree.

## My Script File Is Missing

If you typed a bare name such as:

```text
cow_killer
```

ScriptForge looks for:

```text
%user%/inubot/data/scriptforge/cow_killer.json
```

If the file does not exist, enable `Open editor`, start ScriptForge, build the script, and click `Save`.

## A Block Is Not Running

Check:

- Is the task enabled?
- Is the block enabled?
- Is the block inside an `IF` block that failed?
- Is an earlier blocking task stopping lower tasks from running?
- Is the current task sleeping?
- Does the warnings panel show an error?

## My Else Does Not Run

`Else` only checks the previous sibling block.

Correct:

```text
Find entity target
  Attack variable target
Else
  Walk to coord
```

Wrong:

```text
Find entity target
  Attack variable target
Log message
Else
  Walk to coord
```

In the wrong example, `Else` belongs to `Log message`, not `Find entity`.

## Interact Variable Fails

Check:

- The variable name matches exactly enough to avoid confusion.
- The variable was created earlier in the same task, or has `Global` scope.
- The action is valid for that entity, such as `Attack`, `Take`, `Open`, `Climb`, or `Talk-to`.
- The query actually found something.
- The entity is reachable if it needs to be clicked.

If `Interact variable` is a child of `Find entity`, the variable should exist when the child runs.

## Find Entity Finds Nothing

Check the filters.

Common mistakes:

- Wrong source, such as `Players` instead of `Npcs`.
- Wrong result.
- Empty or misspelled id constants.
- Using exact `Names` when `Name contains` would be easier.
- Requiring an action the entity does not have.
- Using `Not under attack` when every NPC nearby is already in combat.
- Using `Reachable` when the entity is behind an obstacle.

Try fewer filters first. Add filters one by one until it stops finding results.

## The Query Filter Table Feels Empty

Select a source first.

The filter options depend on what kind of thing you are searching. Some filters only make sense for NPCs or players.

## I See Unknown Block Warnings

That usually means the saved script contains a block id that this version of ScriptForge no longer has.

Delete the unknown block and replace it with a current block from the toolbox.

## My Loadout Block Warns About Unknown Loadout

The loadout name must match a saved Inubot loadout.

Check spelling and spacing.

## The Script Keeps Repeating An Action Too Fast

Add `Sleep` after the action.

Example:

```text
Interact variable target
Sleep 2
```

## World Hopping Picks Bad Worlds

Check the `Misc` config.

The hop blocks use `World hop profile`, so fix the profile instead of changing every hop block.

## Webhooks Do Not Send

Check:

- `Webhook URL` is filled in.
- The specific webhook toggle is enabled.
- The event actually happened, such as script stop, ban, or unique item.

If `Webhook URL` is empty, all webhook options are disabled.

## Muling Does Not Happen

Check:

- `Mule enabled` is enabled.
- `Mule key` is correct.
- The Loot tab has items in the `Mule` list.
- Timer settings are correct if you expect timed muling.
- Unique items are listed in the `Uniques` list if you expect unique-triggered muling.

## Membership Does Not Renew

Check:

- `Renew membership` is enabled in the `Misc` config section.
- The account is a regular account.
- A bond is available in the backpack or bank, or the script can buy one.
- The account is in a region where renewal is allowed.

Membership renewal is off by default. It will not redeem or buy bonds unless `Renew membership` is enabled.

## The Best Debugging Habit

Use clear labels.

Instead of:

```text
Find entity
Interact variable
```

Use:

```text
Find goblin
Attack goblin
```

Logs are much easier to read when every important block has a meaningful label.
