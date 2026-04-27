# Game Art & Animation Production Plan (Svenska)

## Mål
Bygga en komplett första leverans för pixel-art produktion till spelet:
- Spelarkaraktär: full animation set + sprite sheet-spec
- Mobs/monster: 4 fiendetyper med animationer + sprite sheet-spec
- Tilesets: terräng, väggar, props och dekoration
- Bakgrunder: 3 parallax-teman
- UI/layout: HUD, inventory-panel och ikoner
- Stencyl-ready importstruktur

> **OBS:** Karaktärens uppladdade bild är ännu inte åtkomlig som fil i repo. Denna leverans innehåller produktionsspecar, naming, frame-data, importmallar och pipelines. När bildfilen lagts i `reference/character.png` kan samma struktur användas direkt för slutproduktion.

---

## 1) Tekniska standarder

- Bas-upplösning: **32x32 px** per frame (karaktär/mobs)
- Boss/large mobs: **48x48 px**
- Target FPS animation: **10–12 fps**
- Color depth: 32-bit PNG (med transparens)
- Pixel-perfect:
  - Ingen anti-aliasing på exports
  - Nearest-neighbor scaling
- Pivot/anchor:
  - Karaktär: bottom-center
  - Flygande mob: center

---

## 2) Spelarkaraktär – animation backlog

### Required set (v1)
- Idle: 6 frames
- Walk: 8 frames
- Run: 8 frames
- Attack_1: 8 frames
- Attack_2: 10 frames
- Hurt: 4 frames
- Death: 10 frames
- Jump: 6 frames
- Fall: 2 frames

### Direction support
- 4-direction (N/S/E/W) i v1
- 8-direction i v2 (diagonaler)

---

## 3) Mobs (för Stencyl)

### Mob A: Slime (32x32)
- Idle 4, Move 6, Attack 6, Hurt 3, Death 6

### Mob B: Skeleton (32x32)
- Idle 6, Walk 8, Attack 8, Hurt 4, Death 8

### Mob C: Bat (32x32, flying)
- Fly 6, Attack 6, Hurt 3, Death 6

### Mob D: Brute/Ogre (48x48)
- Idle 6, Walk 8, Smash 10, Hurt 4, Death 10

---

## 4) Tilesets (för nivåbygge)

### Nature pack
- Grass variants x12
- Dirt transitions x16
- Cliff edges x20
- Water tiles (animated) x8

### Dungeon pack
- Floor variants x12
- Wall blocks x20
- Pillars/doors/traps x18

### Prop pack
- Crates/barrels x8
- Torches (anim) x6
- Signs/fences x10

---

## 5) Bakgrunder (Parallax)

### Theme 1 – Forest
- Sky far
- Mountains mid
- Trees near

### Theme 2 – Cavern
- Ambient fog far
- Stalagmites mid
- Foreground rocks near

### Theme 3 – Ruins
- Moon/sky far
- Ruined arches mid
- Broken pillars near

---

## 6) UI/Layout

- HUD bar (HP/Stamina/Mana)
- Skill slots (1–6)
- Damage popups
- Inventory panel (9x5)
- Pixel icons set (32 ikoner)

---

## 7) Stencyl export-konvention

- Filnamn:
  - `hero_<anim>_<dir>.png`
  - `mob_<name>_<anim>.png`
- Meta-filer:
  - `stencyl/animation_map.csv`
  - `assets/specs/*.json`
- Framerate per anim läses från csv/json

---

## 8) Dagens leveransfönster (17:00–20:00 svensk tid)

För genomgång i kväll:
1. Godkänn stilriktning + frame counts
2. Välj prioritet på mobs (1–4)
3. Bekräfta om 4-direction räcker i v1
4. Ladda karaktärsbild till `reference/character.png`
5. Starta produktion av final sprite sheets enligt spec

