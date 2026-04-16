# Block Reference

This page lists the built-in toolbox blocks.

Most blocks either check something or do something:

- `If...` blocks run their child blocks only when the condition is true.
- Action blocks do something immediately.
- Store/find blocks save a value into a variable.

## Core

| Block | What it does |
| --- | --- |
| `Log message` | Writes a message to the script log. |
| `Sleep` | Sleeps the current task for the provided number of script ticks. |
| `Stop current task (Return)` | Stops the current task from continuing through later sibling blocks this tick. |
| `Else` | Runs child blocks when the previous sibling block failed. |
| `Close interfaces` | Closes visible sub interfaces with close buttons. |
| `If logged in` | Runs child blocks when the game is logged in. |

## Variables

| Block | What it does |
| --- | --- |
| `Set variable` | Stores a text value under a variable name. |
| `If variable equals` | Runs child blocks when a variable equals the provided text. |
| `If variable exists` | Runs child blocks when a variable has a non-null value. |
| `If variable does not exist` | Runs child blocks when a variable has no stored value. |
| `If variable type is` | Runs child blocks when a variable matches a type: NPC, OBJECT, PICKABLE, ITEM, PLAYER, or TEXT. |
| `If variable name contains` | Runs child blocks when a stored game object has a name containing the provided text. |
| `If variable id equals` | Runs child blocks when a stored game object has the provided id. |
| `Interact variable` | Interacts with a stored NPC, object, ground item, or inventory item. |
| `Clear variable` | Removes a stored variable. |

## Entities

| Block | What it does |
| --- | --- |
| `Find entity` | Builds an entity query, stores a result such as first or nearest in a variable, and runs children only when something was found. |

### Entity Query Filters

| Filter | What it does |
| --- | --- |
| `Ids` | Filters by id. Accepts numbers or constants like `NpcId.GOBLIN`, comma-separated. |
| `Name contains` | Filters by partial name. Multiple values can be comma-separated. |
| `Names` | Filters by exact name. Multiple values can be comma-separated. |
| `Actions` | Filters by available action. Multiple values can be comma-separated. |
| `Within distance` | Filters scene entities by distance from the local player. |
| `Targetless` | Filters NPCs or players that are not targeting anything. |
| `Targeting` | Filters NPCs or players that are targeting something. |
| `Has targeters` | Filters NPCs or players based on whether something is targeting them. |
| `Not dying` | Filters entities that expose dying state and are not dying. |
| `Under attack` | Filters NPCs or players with recent incoming attacks. |
| `Not under attack` | Filters NPCs or players without recent incoming attacks. |
| `Attacking` | Filters NPCs or players with recent outgoing attacks. |
| `Reachable` | Filters scene entities whose area is walkable. |

## Game Settings

| Block | What it does |
| --- | --- |
| `If varp equals` | Runs child blocks when a varp equals a value. Varp id can be a number or `VarpId.CONSTANT`. |
| `If varp at least` | Runs child blocks when a varp is greater than or equal to a value. |
| `If varbit equals` | Runs child blocks when a varbit equals a value. Varbit id can be a number or `VarbitId.CONSTANT`. |
| `If varbit at least` | Runs child blocks when a varbit is greater than or equal to a value. |
| `If varc equals` | Runs child blocks when a varc integer equals a value. |
| `If varc at least` | Runs child blocks when a varc integer is greater than or equal to a value. |

## Economy

| Block | What it does |
| --- | --- |
| `Prepare mule` | Triggers the shared framework sell-then-mule flow using the configured loot manifest. |
| `Sell loot` | Triggers the shared framework sell flow using the configured sell loot. |

## Loadouts

| Block | What it does |
| --- | --- |
| `If backpack loadout exists` | Runs child blocks when a saved backpack loadout can be loaded by name. |
| `If equipment loadout exists` | Runs child blocks when a saved equipment loadout can be loaded by name. |
| `If backpack matches loadout` | Runs child blocks when the backpack matches a saved backpack loadout. |
| `If equipment matches loadout` | Runs child blocks when worn equipment matches a saved equipment loadout. |
| `If carrying equipment loadout` | Runs child blocks when the equipment loadout is either worn or present in the backpack. |
| `If loadouts need banking` | Runs child blocks when the backpack loadout is not valid or equipment loadout is not worn or carried. |
| `Withdraw backpack loadout` | Withdraws a saved backpack loadout from the bank. |
| `Withdraw backpack and equipment` | Withdraws a backpack loadout and any missing equipment items together. |
| `Withdraw equipment loadout` | Withdraws missing equipment loadout items into the backpack, skipping items already worn. |
| `Equip loadout` | Equips matching items from the backpack for a saved equipment loadout. |

## Bank

| Block | What it does |
| --- | --- |
| `Bank loadouts` | Opens the bank, withdraws a backpack loadout plus missing equipment, closes the bank, then equips carried equipment. |
| `Open nearest bank` | Walks to and opens the nearest valid bank. |
| `If bank is open` | Runs child blocks when the bank is open. |
| `Close bank` | Closes the bank or other open interfaces. |
| `Deposit inventory` | Deposits all backpack items into the bank. |
| `Deposit equipment` | Deposits all worn items into the bank. |
| `Withdraw item id` | Withdraws an item id from the bank. |
| `Deposit item id` | Deposits an item id from the backpack into the bank. |
| `Set noted withdraw` | Toggles bank withdraw mode to noted or item. |

## Inventory

| Block | What it does |
| --- | --- |
| `If inventory contains item id` | Runs child blocks when the backpack contains at least this many of an item id. |
| `If item id count at most` | Runs child blocks when the backpack contains at most this many of an item id. |
| `Interact inventory item id` | Interacts with the first matching backpack item id. |
| `Store inventory item id` | Stores the first matching backpack item in a variable. Item id can be a number or `ItemId.CONSTANT`. |
| `If inventory contains item name` | Runs child blocks when the backpack contains an item whose name contains the provided text. |
| `If item name count at most` | Runs child blocks when the backpack contains at most this many items whose name contains the provided text. |
| `If has food` | Runs child blocks when the backpack contains an item with an `Eat` action. |
| `Eat food` | Eats the first edible food item in the backpack. |
| `If has prayer potion` | Runs child blocks when the backpack contains a prayer potion or super restore. |
| `Drink prayer potion` | Drinks the first prayer potion or super restore in the backpack. |
| `If inventory is full` | Runs child blocks when the backpack is full. |
| `If inventory is empty` | Runs child blocks when the backpack has no items. |
| `If empty slots at least` | Runs child blocks when the backpack has at least this many empty slots. |
| `Interact inventory item name` | Interacts with the first backpack item whose name contains the provided text. |
| `Store inventory item name` | Stores the first backpack item whose name contains the provided text. |

## Equipment

| Block | What it does |
| --- | --- |
| `If equipment contains item id` | Runs child blocks when worn equipment contains an item id. |
| `If equipment contains item name` | Runs child blocks when worn equipment contains an item whose name contains the provided text. |
| `Remove equipment slot` | Removes the item in an equipment slot. Slots include HEAD, CAPE, NECK, MAINHAND, CHEST, OFFHAND, LEGS, HANDS, FEET, RING, and QUIVER. |

## Movement

| Block | What it does |
| --- | --- |
| `Walk to coord` | Walks to a world coordinate. |
| `If near coord` | Runs child blocks when the local player is within a distance of a coordinate. |
| `If run energy at least` | Runs child blocks when run energy is at least the provided percentage. |
| `Toggle run` | Turns run on or off. |

## Combat

| Block | What it does |
| --- | --- |
| `Attack variable` | Interacts with a stored NPC or player using `Attack`. |
| `If player has target` | Runs child blocks when the local player currently has a combat target. |
| `If target health at most` | Runs child blocks when the local player's combat target has visible health at or below the provided percent. |
| `If in multi-combat` | Runs child blocks when the local player is in a multi-combat zone. |
| `If auto retaliate on` | Runs child blocks when auto retaliate is enabled. |
| `Toggle auto retaliate` | Turns auto retaliate on or off. |
| `If special energy at least` | Runs child blocks when special attack energy is at least the provided percentage. |
| `If special attack active` | Runs child blocks when special attack is currently active. |
| `Toggle special attack` | Turns special attack on or off. |
| `If poisoned` | Runs child blocks when the local player is poisoned or envenomed. |
| `If teleblocked` | Runs child blocks when teleblock is active. |

## Prayer

| Block | What it does |
| --- | --- |
| `If prayer points at least` | Runs child blocks when current prayer points are at least the provided value. |
| `If prayer points at most` | Runs child blocks when current prayer points are at or below the provided value. |
| `If prayer percent at least` | Runs child blocks when current prayer points are at least the provided percentage of base prayer level. |
| `If prayer percent at most` | Runs child blocks when current prayer points are at or below the provided percentage of base prayer level. |
| `If prayer active` | Runs child blocks when a prayer is active. Example: `PROTECT_FROM_MELEE`. |
| `If prayer unlocked` | Runs child blocks when a prayer is unlocked and the player has the level for it. |
| `Toggle prayer` | Turns a prayer on or off. Example: `PROTECT_FROM_MELEE`. |
| `Flick prayer` | Flicks a single prayer. |
| `If quick prayer active` | Runs child blocks when quick prayer is active. |
| `Toggle quick prayer` | Turns quick prayer on or off. |

## Magic

| Block | What it does |
| --- | --- |
| `If can cast spell` | Runs child blocks when the spell is castable. Example: `HIGH_LEVEL_ALCHEMY`. |
| `Cast spell` | Casts a spell with no target. Example: `VENGEANCE`. |
| `Cast spell on variable` | Casts a spell on a stored NPC, player, object, ground item, or inventory item. |
| `If spell selected` | Runs child blocks when any spell is currently selected. |
| `If spell autocast` | Runs child blocks when the provided spell is the current autocast spell. |
| `If home teleport ready` | Runs child blocks when home teleport is not on cooldown. |

## Player

| Block | What it does |
| --- | --- |
| `If player is moving` | Runs child blocks when the local player is moving. |
| `If player is not moving` | Runs child blocks when the local player is loaded and not moving. |
| `If player is animating` | Runs child blocks when the local player has an active animation. |
| `If player is not animating` | Runs child blocks when the local player is loaded and has no active animation. |
| `If player is idle` | Runs child blocks when the local player is not moving and not animating. |
| `If player in area` | Runs child blocks when the local player is inside a rectangular area. |
| `If player not in area` | Runs child blocks when the local player is loaded and outside a rectangular area. |
| `If distance to coord less than` | Runs child blocks when the local player's distance to a coordinate is less than the provided distance. |
| `If distance to coord more than` | Runs child blocks when the local player's distance to a coordinate is greater than the provided distance. |
| `If distance to coord equal to` | Runs child blocks when the local player's distance to a coordinate equals the provided distance. |
| `If nearby player exists` | Runs child blocks when another loaded player is within a distance. |
| `If player in combat` | Runs child blocks when the local player has a target or visible health bar. |
| `If player has target` | Runs child blocks when the local player has a target. |
| `If player has no target` | Runs child blocks when the local player is loaded and has no target. |
| `If player health bar visible` | Runs child blocks when the local player has a visible health bar. |
| `If player health at most` | Runs child blocks when the local player's hitpoints percent is at or below the provided value. |
| `If player health at least` | Runs child blocks when the local player's hitpoints percent is at or above the provided value. |
| `If current hitpoints at most` | Runs child blocks when the local player's current hitpoints are at or below the provided value. |
| `If current hitpoints at least` | Runs child blocks when the local player's current hitpoints are at or above the provided value. |
| `If player overhealed` | Runs child blocks when current hitpoints are above the base hitpoints level. |
| `If player health restored` | Runs child blocks when current hitpoints are at or above the base hitpoints level. |
| `If player animation equals` | Runs child blocks when the local player's animation id equals the provided id. |
| `If player stance equals` | Runs child blocks when the local player's stance animation id equals the provided id. |
| `If player effect active` | Runs child blocks when the local player has an active effect id. Effect id can be a number or `EffectId.CONSTANT`. |
| `If player overhead text contains` | Runs child blocks when the local player's overhead text contains the provided text. |
| `If player overhead prayer active` | Runs child blocks when the local player has the provided overhead prayer icon. Examples: MELEE, RANGE, MAGIC, SMITE. |
| `If player combat level at least` | Runs child blocks when the local player's combat level is at least the provided level. |
| `If player combat level at most` | Runs child blocks when the local player's combat level is at or below the provided level. |
| `If player skulled` | Runs child blocks when the local player has a skull icon. |
| `If player not skulled` | Runs child blocks when the local player is loaded and has no skull icon. |

## Dialog

| Block | What it does |
| --- | --- |
| `If dialog can continue` | Runs child blocks when a continue dialog is visible. |
| `Continue dialog` | Continues the current dialog if possible. |
| `Choose dialog option` | Chooses the first dialog option containing the provided text. |

## Worlds

| Block | What it does |
| --- | --- |
| `Hop specific world` | Hops to a specific world id. |
| `Hop next world` | Hops to the next normal world allowed by the configured world preference profile. |
| `Hop previous world` | Hops to the previous normal world allowed by the configured world preference profile. |
| `Hop random world` | Hops to a random normal world allowed by the configured world preference profile. |
| `If current world is members` | Runs child blocks when the current world is members. |

## Skills

| Block | What it does |
| --- | --- |
| `If base skill level at least` | Runs child blocks when a skill base level is at least the provided level. Skill names are like MAGIC, HITPOINTS, or ATTACK. |
| `If base skill level at most` | Runs child blocks when a skill base level is at or below the provided level. |
| `If current skill level at least` | Runs child blocks when a boosted or current skill level is at least the provided level. |
| `If current skill level at most` | Runs child blocks when a boosted or current skill level is at or below the provided level. |
