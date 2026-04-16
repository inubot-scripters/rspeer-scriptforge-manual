# ScriptForge User Guide

ScriptForge lets you build simple Inubot scripts by arranging blocks instead of writing code.

You create tasks, drag blocks into those tasks, fill in friendly settings, save the script, and then run it. ScriptForge handles the boring shared script features for you, including muling, selling, death handling, optional membership renewal, run toggling, stop handling, webhooks, and common banking helpers.

## Start Here

Read these in order if you are new:

1. [Getting Started](getting-started.md)
2. [Core Concepts](core-concepts.md)
3. [Entities And Queries](entities-and-queries.md)
4. [Default Behaviours](default-behaviours.md)
5. [Loot, Muling, And Shared Features](loot-muling-and-framework.md)
6. [Example Scripts](examples.md)
7. [Troubleshooting](troubleshooting.md)

Keep this one open while building:

- [Block Reference](block-reference.md)

## What You Can Build

ScriptForge is best for scripts made from clear actions and checks:

- Fight an NPC if one is nearby, otherwise walk back to the area.
- Loot specific ground items.
- Bank when your inventory is full or your loadout is missing.
- Withdraw and equip saved loadouts.
- Eat food, drink prayer potions, use prayer, and hop worlds.
- Mule or sell configured loot.
- React to local player state such as moving, animating, health, combat, skull, teleblock, poison, or prayer.

## How Scripts Are Saved

In the script config, you choose a `Script file`.

If you type:

```text
cow_killer
```

ScriptForge saves it as:

```text
<RSPeer data folder>/scriptforge/cow_killer.json
```

You normally do not need to type the folder or `.json`. ScriptForge adds those for you.

## The Main Workflow

1. Set `Script file`.
2. Turn on `Open editor`.
3. Start the script.
4. Build your script in the editor.
5. Click `Save`.
6. Stop the script.
7. Turn off `Open editor`.
8. Start the script again to run it.

Edit mode opens the editor. Run mode executes the saved script.
