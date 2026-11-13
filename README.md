# CutVisor — Timber Cut Optimizer for Blender

**design & craft with minimum waste**

CutVisor is a Blender addon for timber structure projects. Assign part IDs to your components, calculate mass/volume/cost, export Bills of Materials, generate an optimized cut plan with printable cut sheets, and work out paint, primer and treatment quantities — so you know exactly what to buy and how to cut it.

📖 **[User guide](https://raduandrei-source.github.io/CutVisor/)** (English, Français, Español, Português)

![CutVisor hero](CutVisor%20hero.png)

---

## Free vs Pro

| Feature | Core (free) | Pro |
|---|---|---|
| Materials & Stock Sizes | ✓ | ✓ |
| Generate Part IDs | ✓ | ✓ |
| Detailed & Consolidated BOM export | ✓ | ✓ |
| Shopping List generation | ✓ | ✓ |
| Kerf, Stock Bonus, Tolerance settings | ✓ | ✓ |
| Viewport overlay (IDs, names, dims, count) | ✓ | ✓ |
| View presets (All / IDs / Dims / Off) | ✓ | ✓ |
| Convert GN Array → Legacy | ✓ | ✓ |
| Diagnose Active Object | ✓ | ✓ |
| Lists CSV export | ✓ | ✓ |
| Cut Sheets — printable SVG + DXF of every board | ✓ | ✓ |
| Identify mode — click a piece in the report, find it in the viewport | ✓ | ✓ |
| Hardware list (manual) in the Shopping List and BOM | ✓ | ✓ |
| Finishes: area to finish (m², end grain separately) | ✓ | ✓ |
| Help (?) and settings menu (gear) in the panel header | ✓ | ✓ |
| Multi-language UI (14 languages) | ✓ | ✓ |
| **Rip Cut, Cross-Cut, Long Rip settings** | — | ✓ |
| **Width Variation** | — | ✓ |
| **Multi-Board Splicing** | — | ✓ |
| **Wood species density presets** | — | ✓ |
| **Overlay: color, shadow, outline** | — | ✓ |
| **CSV import (materials & stock)** | — | ✓ |
| **Finishes: products, finish systems, quantities, packages and costs** | — | ✓ |
| **Finishes: species absorption (EN 350) and surface grade** | — | ✓ |
| **Finishes: Maintenance mode — exposed faces only** | — | ✓ |
| **Finishes in the Shopping List and BOM exports** | — | ✓ |

👉 **[Get CutVisor Pro on Gumroad →](https://cutvisor.gumroad.com/l/yiqahd)**

---

## Installation

1. Download the latest `cutvisor.x.y.z.zip` from [Releases](../../releases)
2. In Blender 4.2 and newer: **Edit → Preferences → Add-ons → ⌄ (top right) → Install from Disk…**
   (Blender 4.0–4.1: **Edit → Preferences → Add-ons → Install…**)
3. Select the zip file
4. Enable **CutVisor** in the add-ons list
5. Open the **N-panel** in any 3D Viewport → **CutVisor** tab

> **Updating:** remove the old version first (Add-ons → CutVisor → ⌄ → Uninstall), restart Blender, then install the new zip.
>
> **Pro users:** click the gear (⚙) in the CutVisor panel header → **License** → paste or enter your activation key → Pro features unlock instantly.

---

## Quick Start

### 1. Add a material
Go to **Materials tab** → **+** → set name, density, pricing mode and stock sizes.

### 2. Assign materials to objects
Select your mesh objects → Materials tab → **Assign to Selected**.

### 3. Generate Part IDs
**Parts tab** → **Generate Part IDs** — assigns a unique ID to each piece and reads dimensions automatically.

The status bar shows how many objects have IDs and flags any without a material assigned.

### 4. Export BOM
**Planning tab** → **Export Detailed BOM** or **Export Consolidated BOM** — saves a CSV file next to your .blend file.

### 5. Generate Shopping List
**Planning tab** → set kerf, stock bonus and tolerance → **Generate Shopping List** — runs the cut optimizer; **Export CSV** saves a timestamped file with the full cut plan.

### 6. Print the cut sheets
**Planning tab** → **Export Cut Sheets** — an SVG diagram of every board (to scale, with Part IDs and cut order) and a DXF for CNC or panel saws.

### 7. Finishes (optional)
**Finishes tab** → **Calculate area (selection)** gives the surface to paint or treat. With Pro, define products and finish systems and get the quantities, the packages to buy and their cost — for a new build or for maintenance of an existing structure. See the [user guide](https://raduandrei-source.github.io/CutVisor/) for details.

---

## Supported Modifiers

CutVisor reads instance counts and dimensions from:

- **Array (Fixed Count)** — count read directly from modifier
- **Array (Fit Length)** — count estimated from evaluated mesh
- **Mirror** — axes read from modifier parameters
- **Geometry Nodes** — count cannot be auto-detected; set manually in the Parts list

---

## Compatibility

- Blender **4.0 and newer**, including **5.x** (v1.0.2 tested on 4.1 – 5.3)
- Windows, macOS, Linux
- Metric and Imperial units

---

## Language Support

CutVisor ships with translations for **14 languages:**
English · Français · Deutsch · Română · Polski · Español · Italiano · Português · Русский · 中文 · 日本語 · 한국어 · العربية · Türkçe

To add a new language or fix a translation:
1. **Gear menu (⚙) → Translations CSV → Export**
2. Add a new column with your language name
3. Fill in the translations
4. **Gear menu (⚙) → Translations CSV → Import**

---

## File Structure

```
cutvisor/
  __init__.py    — Blender addon registration & bl_info
  addon.py       — All addon logic (~12,500 lines)
```

---

## Changelog

### v1.0.2
- New: **Finishes** tab — paint, primer and treatment quantities from the 3D model
  - Core: area to finish for the selected pieces (m², end grain separately, Array/Mirror instances counted)
  - Pro: products (biocide, fire retardant, primer, paint/varnish) with datasheet consumption and package sizes; finish systems assigned per material or per object; species absorption (EN 350) and surface grade (rough / planed / sanded); a primer lowers the consumption of the paint on top; cheapest package combination and costs; library shared between projects
  - Pro: **Maintenance mode** — only the faces that do not touch other parts are counted (joints and contacts are skipped), with surface condition and a hidden-face preview in the viewport
  - Pro: FINISHES section in the Shopping List and Consolidated BOM, finish columns in the Detailed BOM
- New: **Cut Sheets** — printable SVG diagram and DXF R12 of every board, to scale, with Part IDs, numbered cut order and hatched waste
- New: **Identify mode** — expand a board in the Shopping List report and click a piece to select it in the viewport, with a single temporary label
- New: **Hardware list (manual)** — screws, bolts, hinges with quantities and prices, added to the Shopping List and Consolidated BOM CSV
- New: **help (?)** and **settings (gear)** buttons in the panel header — help opens the user guide at the section for the current tab; the gear menu replaces the Settings tab (tabs are now Materials · Parts · JARCH / Planning · Finishes · View)
- New: Fir and Douglas fir species presets
- Fixed: the species preset selector did not reset after a preset was applied (Blender 5.x)

### v1.0.1
- New: Volume Filter (Parts tab) — live volume readout, Min/Max range select/exclude, "Select Same Volume" with adjustable tolerance
- New: dedicated JARCH Import tab, separated from Parts; tab bar now spans two rows for readability
- Improved: L×W×T dimension measurement reworked to use face area instead of vertex positions — fixes incorrect dimensions on bevelled, rotated, or inconsistently-modelled pieces
- Improved: Shift-click to extend selection in the Shopping List's Unmatched section, with highlighting for currently-selected rows

### v1.0.0
- Initial release
- Core: Materials, Stock Sizes, Part IDs, BOM export, viewport overlay, Shopping List with FFD cut optimizer
- Pro: CSV import, advanced overlay styling, wood presets, width variation, rip/cross-cut limits, multi-board splicing, JARCH Vis import

---

## License

CutVisor uses a dual license model:

### Core — GNU General Public License v3.0

The CutVisor Core addon code is free software: you can redistribute it
and/or modify it under the terms of the GNU General Public License as
published by the Free Software Foundation, either version 3 of the
License, or (at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

See the full license text at: https://www.gnu.org/licenses/gpl-3.0.html

### Pro Features — Commercial License

The Pro features of CutVisor (CSV import for materials and stock,
advanced overlay styling, wood species presets, width variation and
rip/cross-cut limits, multi-board splicing, JARCH Vis import, the Finishes
module (products, finish systems, quantities and maintenance mode), and all
features unlocked by a `CWTW-…` activation key) are **not covered by the GPL**.

By purchasing a Pro key you agree to the following terms:

- The key is a **single-user, non-transferable** license
- You may install and use CutVisor Pro on computers you personally own or control
- **Redistribution of Pro activation keys is strictly prohibited**
- Reverse-engineering or bypassing the activation system to unlock Pro
  features without a valid key is not permitted
- The Pro license does not expire; future updates are provided at the
  author's discretion

To purchase a Pro key: [CutVisor Pro on Gumroad](https://cutvisor.gumroad.com/l/yiqahd)

---

## Links

- 🛒 [CutVisor Pro on Gumroad](https://cutvisor.gumroad.com/l/yiqahd)
- 📖 [User guide](https://raduandrei-source.github.io/CutVisor/)
- 🎬 [Video demo on YouTube](https://youtu.be/TOB81vilmtw)
- 🐛 [Report a bug](../../issues)
- 💬 [Discussions](../../discussions)
