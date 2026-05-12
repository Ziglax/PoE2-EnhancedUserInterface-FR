# PoE2 Enhanced User Interface — French Translation

French translation of [PoE2 Enhanced User Interface](https://github.com/Spherikal/PoE2-EnhancedUserInterface) by **Spherikal** (also on [Nexus Mods](https://www.nexusmods.com/pillarsofeternity2/mods/32)).

This is an **unofficial translation patch**. It contains only the localized `.stringtable` files; the original mod is still required to install the gameplay logic, sprites, and metadata.

Target mod version: **1.7.3** (the latest release at time of translation).

---

## What's included

Five `.stringtable` files covering every text entry the mod enhances:

| File | Entries |
|---|---|
| `abilities.stringtable` | 830 |
| `cyclopedia.stringtable` | 93 |
| `gui.stringtable` | 137 |
| `items.stringtable` | 112 |
| `statuseffects.stringtable` | 349 |

Each French entry mirrors the English structure of the original mod — same `<link>`, `<color>`, `<sprite>`, `<voffset>`, `<size>` tags — so in-game tooltips render with the full color-coded keyword highlighting, sprite icons, and glossary links that the mod provides.

---

## Installation

1. **Install the original mod first**, following [Spherikal's instructions](https://github.com/Spherikal/PoE2-EnhancedUserInterface#installation).
   The mod lives under `Pillars of Eternity II\PillarsOfEternityII_Data\override\PoE2-EnhancedUserInterface\`.
2. From this repository, copy the contents of `localized/fr/` into the mod folder, so you end up with:
   ```
   PoE2-EnhancedUserInterface/
   └── localized/
       ├── en/
       │   └── text/game/*.stringtable      (original, untouched)
       └── fr/
           └── text/game/*.stringtable      (this translation)
   ```
3. Launch the game with French selected as the text language. The mod's enhanced tooltips will render in French.

To revert, simply delete the `localized/fr/` folder — the mod falls back to English automatically.

---

## Translation methodology

The translation was built incrementally with a custom PowerShell toolchain. The process aimed at **structural parity with the English source**: every `<link>` URL, every color block, and every sprite that the original mod injects had to appear in the French version too, otherwise the in-game tooltip falls back to plain text and the enhancement is lost.

### 1. Baseline: official French game text

The game ships with an official French translation in `game_FR/*.stringtable`. For every entry the mod modifies, the official French sentence was used as the starting point — guaranteeing terminological consistency with the rest of the game (Déviation, Robustesse, Réflexes, Volonté, Précision, Santé, Valeur d'armure, etc.).

### 2. Single-word link substitution (V2)

A first-pass script walked every `<link="…">word</link>` block in the English mod, extracted the keyword, mapped it to its official French form via a glossary derived from the base game, and rewrapped the matching French word with the corresponding link/color/sprite block.

This covered the majority of single-keyword highlights (damage types, status effects, defense names) but skipped entries where the French word wasn't a direct substring match.

### 3. Pattern-driven multi-keyword insertion (V3 patterns)

For recurring composite patterns — most notably the four-defense list `(Deflection, Fortitude, Reflex, and Will)` that appears in 34+ entries — a JSON-driven pattern engine (`v3-defense-patterns.json` + `v3-fix-defenses.ps1`) inserted the full enriched block in one shot, preserving the EN sprite/color sequence.

### 4. Full-entry rewrites (V3 rewrites)

Entries that diverged semantically from the EN — or that had been corrupted by an earlier round-trip through cp1252 (~30 entries where French accents had become `U+FFFD` replacement characters) — were rewritten end-to-end against the EN structure. The manifest `v3-rewrite-data.json` accumulated 114 such rewrites across the five files.

### 5. Diagnostic loop

After every batch, a diagnostic script (`v2-diag-all.ps1`) counted, per URL, how many `<link>` blocks existed in EN vs FR for each entry. Any URL with a deficit was a "miss". The fix → diag → fix cycle continued until the miss count reached zero on all four mod-extended files.

### 6. Final coherence check (V4)

A last pass cross-validated the result against three sources — `en_ui/`, `game_EN/`, `game_FR/`:

- ID parity between EN and FR mod files (no orphan entries)
- No mojibake (`Ã©`, `Â°`, …) or U+FFFD replacement chars
- Tag balance: `<link>`, `<b>`, `<font>`, `<size>`, `<voffset>` open and close counts match the EN equivalent
- Length divergence vs `game_FR` (catches accidental truncation)
- Glossary terminology aligned with the official French game vocabulary

Final state: **0 anomalies across all 5 files**.

---

## Credits

- **Spherikal** — author of the original [PoE2 Enhanced User Interface](https://github.com/Spherikal/PoE2-EnhancedUserInterface) mod (and the team credited there: Xaratatas, Kilay, Ethics Gradient, commonterry, peardox).
- **Obsidian Entertainment** — original French localization of *Pillars of Eternity II: Deadfire*, used as the terminological baseline.

This translation is offered as a community contribution under the same terms as the original mod. If the upstream author requests removal or changes, please open an issue.

---

## Reporting issues

If a tooltip displays oddly in-game (missing color, broken sprite, untranslated keyword), open an issue with:

- The entry context (which ability / item / cyclopedia article)
- A screenshot if possible
- The mod version you're running

Pull requests with corrections are welcome.
