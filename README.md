# PoE2 Enhanced User Interface — French Translation

Unofficial French translation patch for [PoE2 Enhanced User Interface](https://github.com/Spherikal/PoE2-EnhancedUserInterface) by **Spherikal** ([Nexus page](https://www.nexusmods.com/pillarsofeternity2/mods/32)).

Target mod version: **1.8.2**.

## Contents

Five `.stringtable` files, **1521 entries** translated:

| File | Entries |
|---|---|
| `abilities.stringtable` | 830 |
| `statuseffects.stringtable` | 349 |
| `gui.stringtable` | 137 |
| `items.stringtable` | 112 |
| `cyclopedia.stringtable` | 93 |

Each French entry mirrors the English structure (same `<link>`, `<color>`, `<sprite>` tags), so the mod's color-coded tooltips render correctly in French.

## Installation

1. Install the [original mod](https://github.com/Spherikal/PoE2-EnhancedUserInterface) first.
2. Copy `localized/fr/` from this repository into the mod folder, alongside the existing `localized/en/`.
3. Set the game's text language to French.

## Methodology

Generated with **Claude Opus 4.7** through a custom PowerShell toolchain that combined:

- the official French strings of *Pillars of Eternity II: Deadfire* (extracted from the game) as the terminology baseline
- automated link/color/sprite tag injection mirroring the English mod structure
- a diagnostic loop iterating fix → verify until full structural parity (0 anomalies, 0 missing tags, 0 encoding artifacts).

## Credits

- **Spherikal** and contributors — original mod
- **Obsidian Entertainment** — official French localization used as terminology reference

Issues and pull requests welcome.
