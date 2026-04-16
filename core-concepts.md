# Core Concepts

This page explains how ScriptForge thinks.

## Tasks

A task is a top-level script routine.

Examples:

- `Fight goblins`
- `Loot arrows`
- `Bank`
- `Emergency hop`

Tasks run from top to bottom. Task order is important because earlier tasks get checked first.

Each task has settings:

- `Name`: what you see in the graph and logs.
- `Enabled`: disabled tasks do not run.
- `Blocking`: when a blocking task runs successfully, lower tasks do not get a turn that tick.
- `Block if sleeping`: if the task is sleeping, it can still block lower tasks.

For most simple scripts, keep important safety or banking tasks above normal activity tasks.

## Blocks

Blocks are the steps inside a task.

There are two common block shapes:

- `IF`: checks something. Child blocks only run when the check passes.
- `DO`: performs an action and usually has no children.

Example:

```text
If inventory is full
  Open nearest bank
  Deposit inventory
```

The bank blocks only run when the inventory is full.

## Block Order

Blocks run from top to bottom.

If a block has children, those children run before ScriptForge moves to the next sibling block.

Example:

```text
If player health at most 40
  Eat food
Find entity target
  Attack variable target
```

This checks health first. If health is low, it eats. Then it looks for a target.

## Else

`Else` runs when the previous sibling block failed.

Example:

```text
Find entity target
  Attack variable target
Else
  Walk to coord
```

This means:

- If ScriptForge finds `target`, attack it.
- If ScriptForge does not find `target`, walk somewhere.

`Else` must be directly after the block it belongs to.

## Sleep

`Sleep` pauses the current task for a number of script ticks.

Use it after actions that should not be spammed every tick.

Example:

```text
Interact variable target
Sleep 2
```

Each visual task has its own sleep. Sleeping one task does not sleep every other task.

## Variables

A variable is a saved name for something.

Common examples:

- `target`: the NPC you found.
- `loot`: the ground item you found.
- `door`: the object you found.

You usually create variables with `Find entity`.

Example:

```text
Find entity target
  Interact variable target
```

The first block stores an NPC, object, player, ground item, or other result under the name `target`. The child block uses that saved thing.

## Variable Scope

Scope controls where a variable can be used.

- `Task`: default. Available to later blocks in the same task.
- `Branch`: only available inside the children of the block that created it.
- `Global`: available across tasks.

Use `Task` most of the time.

Use `Branch` when a variable should only exist inside a successful `Find entity`.

Use `Global` only when another task really needs the same value.

## Constants

Some fields ask for ids. You can type raw numbers, but constants are easier to read.

Examples:

- `ItemId.COINS`
- `ItemId.LOBSTER`
- `NpcId.GOBLIN`
- `ObjectId.BANK_BOOTH`
- `EffectId.VENGEANCE`
- `AnimationId.HUMAN_DANCE`

You can also use comma-separated lists in query filters:

```text
NpcId.GOBLIN, NpcId.GOBLIN_2
```

## Labels

Every task and block can have a label.

Labels are for humans. They make the graph easier to read and make logs clearer.

Good labels:

- `Find goblin`
- `Attack goblin`
- `Walk back to cows`
- `Eat below 40 percent`

Duplicate labels are allowed, but unique labels make debugging much easier.

## Disabled Blocks

Disabled blocks stay in the script but do not run.

This is useful when testing. You can temporarily disable a block instead of deleting it.

