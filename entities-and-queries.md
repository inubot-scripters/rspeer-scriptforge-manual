# Entities And Queries

Entities are things in the game world.

Examples:

- NPCs, such as goblins or dragons.
- Players.
- Objects, such as doors, ladders, or bank booths.
- Ground items.
- Projectiles and effect objects.
- Interfaces, stock market entries, and trade items.

ScriptForge uses `Find entity` to search for one of these things, store it in a variable, and then run child blocks when it was found.

## The Find Entity Block

`Find entity` has four important settings:

- `Variable`: the name to save the result as, such as `target`.
- `Scope`: where that saved value can be used.
- `Source`: what kind of thing to search.
- `Result`: which result to keep.

Common sources:

- `Npcs`
- `SceneObjects`
- `Players`
- `Pickables`
- `EffectObjects`
- `Projectiles`
- `Interfaces`
- `StockMarket`

Common results:

- `nearest`
- `furthest`
- `first`
- `last`
- `random`

Only results that return one thing are shown. Results that need extra hidden settings are skipped.

## Query Filters

Filters narrow the search.

Common filters:

- `Ids`: match ids or constants, such as `NpcId.GOBLIN`.
- `Names`: match exact names.
- `Name contains`: match partial names.
- `Actions`: require an action such as `Attack`, `Take`, `Open`, or `Climb`.
- `Within distance`: only things near your player.
- `Reachable`: only things that can be walked to.
- `Targetless`: NPCs or players that are not targeting anything.
- `Targeting`: NPCs or players that are targeting something.
- `Has targeters`: whether something is targeting that entity.
- `Not dying`: removes dying entities.
- `Under attack`: entities with recent incoming attacks.
- `Not under attack`: entities without recent incoming attacks.
- `Attacking`: entities with recent outgoing attacks.

You can combine filters.

Example target search:

```text
Find entity target
  Source: Npcs
  Result: nearest
  Filters:
    Names: Goblin
    Actions: Attack
    Reachable
    Not dying
    Not under attack
```

## Attack A Found NPC

Use this pattern:

```text
Find entity target
  Interact variable target
    Action: Attack
```

Or:

```text
Find entity target
  Attack variable target
```

`Attack variable` is just a shortcut for attacking a stored NPC or player.

## Walk Somewhere If Nothing Was Found

Use `Else` directly after `Find entity`.

```text
Find entity target
  Attack variable target
Else
  Walk to coord
```

This means:

- Found target: attack.
- No target: walk.

## Loot A Ground Item

Use `Pickables` as the source.

```text
Find entity loot
  Source: Pickables
  Result: nearest
  Filters:
    Ids: ItemId.BONES
    Actions: Take
    Reachable
  Interact variable loot
    Action: Take
```

## Use Names Or Ids?

Prefer ids when possible.

Names are easy to understand, but ids are more exact and work better with noted items or items that share similar names.

Good examples:

- `ItemId.COINS`
- `ItemId.BONES`
- `NpcId.GOBLIN`
- `ObjectId.BANK_BOOTH`

## Variable Checks

If a later block may or may not have a variable, guard it:

```text
If variable exists target
  Attack variable target
```

Or use the opposite:

```text
If variable does not exist target
  Walk to coord
```

Most of the time, if `Interact variable` is a child of `Find entity`, you do not need a separate exists check.

