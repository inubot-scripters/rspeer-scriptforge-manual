# Example Scripts

These examples are written as flow outlines. Build them by creating tasks and adding the named blocks in the same shape.

## Goblin Fighter

Goal:

- Eat when low health.
- Attack a nearby goblin.
- Walk back to the goblin area if none are found.

Task: `Survive`

```text
If player health at most
  Percent: 45
  Eat food
```

Task: `Fight goblins`

```text
Find entity
  Label: Find goblin
  Variable: target
  Scope: Branch
  Source: Npcs
  Result: nearest
  Filters:
    Names: Goblin
    Actions: Attack
    Reachable
    Not dying
    Not under attack
  Attack variable
    Variable: target
Else
  Walk to coord
    X: your goblin area x
    Y: your goblin area y
    Z: 0
```

Notes:

- Put `Survive` above `Fight goblins`.
- Use labels like `Find goblin`, `Attack goblin`, and `Walk back`.
- If every goblin is already in combat, remove `Not under attack`.

## Loot Bones

Goal:

- Take nearby bones when they are visible.

Task: `Loot bones`

```text
Find entity
  Label: Find bones
  Variable: loot
  Scope: Branch
  Source: Pickables
  Result: nearest
  Filters:
    Ids: ItemId.BONES
    Actions: Take
    Reachable
  Interact variable
    Variable: loot
    Action: Take
```

Notes:

- `Pickables` means ground items.
- Use `ItemId` constants where possible.

## Bank When Inventory Is Full

Goal:

- Walk to the nearest bank.
- Deposit everything.

Task: `Bank full inventory`

```text
If inventory is full
  Open nearest bank
  If bank is open
    Deposit inventory
    Close bank
```

Notes:

- Put this above your normal fighting or gathering task.
- If the task is blocking, it can stop lower tasks while banking.

## Bank A Saved Loadout

Goal:

- If your backpack or equipment loadout is wrong, bank and fix it.

Task: `Fix loadout`

```text
If loadouts need banking
  Backpack: your backpack loadout name
  Equipment: your equipment loadout name
  Bank loadouts
    Backpack: your backpack loadout name
    Equipment: your equipment loadout name
```

Notes:

- Loadout names must match saved Inubot loadouts.
- The warnings panel will tell you if a loadout name is unknown.

## Hop When A Player Is Nearby

Goal:

- Hop if another player is close.

Task: `Safety hop`

```text
If nearby player exists
  Distance: 12
  Hop random world
```

Notes:

- The hop uses the `World hop profile` from Misc config.
- Put safety tasks high in the task list.

## Use Prayer In Combat

Goal:

- Turn on a prayer if you have enough prayer points.

Task: `Prayer`

```text
If prayer points at least
  Points: 5
  Toggle prayer
    Prayer: PROTECT_FROM_MELEE
    Enabled: true
```

Notes:

- Prayer names use dropdown suggestions.
- `If prayer unlocked` can be used before toggling if the script may run on different accounts.

## Sell Or Mule Loot

Goal:

- Use shared framework economy.

Setup:

- Add items in the `Loot` tab.
- Enable `Mule enabled` if you want muling.
- Fill in `Mule key` if your mule setup requires it.

Task: `Mule`

```text
Prepare mule
```

Or if you only want selling:

```text
Sell loot
```

Notes:

- `Prepare mule` uses the Loot tab and Muling config.
- Unique items listed in the Loot tab can trigger muling when muling is enabled.

