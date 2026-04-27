# Idle Action RPG – Systemdesign (Svenska)

## Syfte
Detta dokument kompletterar befintliga sprite- och tileset-specar med spelmekanik för **idle gameplay**:
- Auto walk/patrol
- Auto attacks
- Klassval (Warrior, Mage, Archer)
- Spells inklusive AOE
- Tydliga animationskrav per state

## Core loop (Idle)
1. Spelaren väljer klass.
2. Karaktären auto-walkar längs lane/waypoints.
3. När fiende är inom räckvidd triggas auto attack.
4. Mana byggs upp passivt + on-hit.
5. Spell eller AOE används enligt cooldown-prioritet.
6. Loot/xp samlas automatiskt.
7. Progression låser upp nya spells och animationsnivåer.

## Auto Walk (spec)
- Mode: `lane_loop` eller `waypoint_pingpong`
- Hastighet: klassberoende
  - Warrior: 1.00x
  - Mage: 0.95x
  - Archer: 1.10x
- Stop condition:
  - Fientlig enhet inom aggro-range
  - Boss trigger zon
- Resume condition:
  - Inga fiender i range under 1.2 sek

## Auto Attack (spec)
- Prioritet:
  1) Fiende som attackerar spelaren
  2) Lägst HP inom range
  3) Närmaste fiende
- Target lock timeout: 1.0 sek
- Windup/winddown måste mappas till animation events.

## Klassöversikt

### Warrior
- Roll: frontline/bruiser
- Grundattack: melee cleave
- Resurs: rage
- Signatur-AOE: `Whirlwind`

### Mage
- Roll: burst/control
- Grundattack: magic bolt
- Resurs: mana
- Signatur-AOE: `Arcane Nova`

### Archer
- Roll: sustained DPS/kiting
- Grundattack: arrow shot
- Resurs: focus
- Signatur-AOE: `Volley Rain`

## Spell-logik
- Spell queue (auto-cast):
  - Cast första spell vars `cooldown == 0` och `resource >= cost`.
  - Om flera: välj högst `priority`.
- AOE target cap:
  - Standard: 5 targets
  - Boss scenario: obegränsat men falloff skada efter target 3
- Cooldown reduceras av haste stat men aldrig under 35% av base cooldown.

## Animation states (obligatoriska)
- `idle`
- `auto_walk`
- `auto_attack`
- `cast_start`
- `cast_loop` (kan hoppas över på instant spells)
- `cast_release`
- `aoe_cast`
- `hurt`
- `death`
- `victory`

## Animation quality gates
- Läsbar silhouette i 1x och 2x skala
- Max 1 huvud-action per frame
- Impact frame för attack/spell release
- VFX sync via event tags: `HIT`, `PROJECTILE_SPAWN`, `AOE_RELEASE`

## Stencyl-integration
- Behaviors:
  - `AutoWalkController`
  - `AutoAttackController`
  - `AutoCastController`
  - `ClassLoadoutController`
- Data-driven setup från:
  - `assets/specs/classes/*.json`
  - `assets/specs/effects/spells_spec.json`
  - `assets/specs/gameplay/auto_systems_spec.json`

