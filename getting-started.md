# Getting Started

This page assumes you have never written code. You only need to understand the editor.

## Create A Script File

Open the script config before starting ScriptForge.

Set:

- `Script file`: the name of your script, such as `cow_killer`.
- `Open editor`: enabled.

Then start ScriptForge.

If `Script file` is `cow_killer`, the saved file will be:

```text
<RSPeer data folder>/scriptforge/cow_killer.json
```

You can also use folders:

```text
combat/cow_killer
```

That saves under:

```text
<RSPeer data folder>/scriptforge/combat/cow_killer.json
```

## Editor Layout

The editor has three main tabs:

- `Editor`: build tasks and blocks.
- `Loot`: configure sell items, mule items, and unique items.
- `Guide`: quick reminders inside the app.

The `Editor` tab has several areas:

- `Toolbox`: blocks and recipes you can add.
- `Inspector`: settings for the selected task or block.
- `Warnings`: problems ScriptForge found.
- `Variables`: saved names such as `target` or `loot`.
- `Graph`: the visual script flow window.

If you close the graph, click `Show Graph` to open it again.

## Shared Config Defaults

ScriptForge has shared config sections under the normal script config:

- `Misc`: world hopping, poor proxy behavior, and optional membership renewal.
- `Muling`: mule key, coin requests, unique-triggered muling, and timer-triggered muling.
- `Webhook`: optional messages for stops, bans, and uniques.

Important defaults:

- Membership renewal is off unless `Renew membership` is enabled.
- Muling is off unless `Mule enabled` is enabled.
- If muling is enabled, unique-item muling is enabled by default and uses the `Uniques` list in the Loot tab.
- Timer muling only happens when `Trigger on timer` is enabled.
- Empty timer hours default to `4` hours when timer muling is enabled.
- Empty reverse-mule coin amount defaults to `5000000` coins when muling is enabled.
- Death handling is on by default for normal Death's Domain recovery.
- Run toggling is on by default and turns run on around `20` to `30` energy.
- Restocking is available by default when loadout items have restock data.

For the full list, read [Default Behaviours](default-behaviours.md).

## Your First Task

A task is a group of blocks that runs repeatedly.

To create one:

1. Click `New Task`.
2. Select the task in the graph.
3. Rename it in the inspector, for example `Fight goblins`.
4. Make sure it is enabled.

Task order matters. Higher tasks run first.

## Add Blocks

Use the toolbox to add blocks:

- Double-click a block to add it quickly.
- Drag a block onto the graph.
- Right-click the graph for copy, paste, duplicate, delete, snippets, and enable/disable.
- Select a block to edit its settings in the inspector.

Most blocks are one of two types:

- `IF` blocks check something and only run their child blocks when the check passes.
- `DO` blocks do an action, such as walking, attacking, eating, or banking.

## Save And Run

When the script looks right:

1. Click `Save`.
2. Stop ScriptForge.
3. Open the script config.
4. Disable `Open editor`.
5. Start ScriptForge again.

Now it runs the saved script instead of opening the editor.

## Useful Keyboard Shortcuts

- `Ctrl+Z`: undo.
- `Ctrl+Shift+Z`: redo.
- `Ctrl+N`: new task.
- `Ctrl+R`: rename selected task or block.
- `Delete`: delete selected task or block.
- `Ctrl+C`: copy selected block and its child blocks.
- `Ctrl+Shift+C`: copy only the selected block, without its children.
- `Ctrl+V`: paste copied block.
- `Up` / `Down`: reorder the selected task or block.

## Warnings Are Your Friend

The warnings panel can catch common mistakes:

- Empty tasks.
- Unknown blocks.
- Missing script file.
- Unknown loadout name.
- Variable names that were never created.
- Invalid constants such as a misspelled `ItemId` or `NpcId`.
- Empty query filters.

If something does not work, check warnings first.
