# Arma 3

## Table of Contents
+ [Triggers](#triggers)
+ [Systems](#systems)
+ [Waypoints](#waypoints)
+ [Configuration](#configuration)
+ [Others](#others)


## Triggers

Link triggers to whatever you want to activate (example: presence trigger linked to a respawn system).

**Trigger activated by BLUFOR presence**:
- Size: Set area
- Variable name: Set a unique name.
- Type: Guarded by OPFOR
- Activation: BLUFOR
- Activation type: Present
- Condition: this
- Interval: 1
- Effect condition: true / Sound: Alarm

**Victory trigger**:
- Type: End#1
- Activation: none
- Condition: `(triggerActivated trigger_1) && (triggerActivated trigger_2) && ... && (triggerActivated trigger_n)`
- Interval: 10

**Guarded area**: A close team will guard it. If it's eliminates, another close team will replace it.
- Set area size
- Type: Guarded by OPFOR


## Systems

**Vehicle respawn**:
Type: Multiplayer/Vehicle respawn
Probability of presence: 100%
Condition of presence: true
Delay: 60
Deserted distance: 200
Position: Starting position
Wreck: Delete with an explosion

**Conquered player respawn**: Linked to a presence trigger (except those not conquerable). Playable characters are configured as "player".
Type: Multiplayer/Respawn position
Probability of presence: 100%
Condition of presence: true
Type: Infantry
Side: BLUFOR
Show to: Everyone


## Waypoints

**Guard waypoint*: Assign it to a team that you want to stay in a position.


## Configuration

**Attributes/General**:
- DLC: None
- States
- Misc: Don't binarize scenario file

**Attributes/Environment**: Weather configuration

**Attributes/Multiplayer**:
- Game type: Undefined game type
- Enable AI: Yes or not
- Respawn: Respawn (respawn on custom position), rulesets (select respawn position / show respawn counter), respawn delay, vehicle respawn delay, show scoreboard, allow manual respawn.
- Revive: Mode (enabled for all players), trait (none), items (none), duration (0:06), medic multiplier (x2), force respawn duration (0:10), incapacitation mode (basic), duration (2:00).


## Others

**Invincible player**:
- Init: `this addEventHandler [ "handleDamage", {false} ]`



