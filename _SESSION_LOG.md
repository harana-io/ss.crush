# D&D / Pathfinder 2e — Session Log
(Newest entry on top.)

## 2026-08-11 (later)

- **Did:** Named the character **Cat the Bounty Hunter**. Built two interactive companions to the markdown build: `Pathfinder 2e/character-sheet.html` (dice roller with degrees of success, HP/hero-point trackers, sneak-attack toggle, MAP selector) and `Pathfinder 2e/character-3d.html` (full-body 3D model). The 3D model started as a flat-shaded canvas renderer, then was rewritten in **WebGL** for smooth per-pixel-lit surfaces — every part is a lathe or parametric sheet with averaged normals, so there are no facets.
- **Added:** four keyframed fight clips — Lunge, Slash, Feint, and **The Gambit**, which animates the actual PF2e turn: Feint → free Step → Strike → Strike. Plus stances, a Repeat toggle, three lighting rigs, and a loadout rail that highlights parts on the model.
- **Bugs found and fixed (worth remembering):**
  - **Tail sat on his chest.** `rotX(+a)` tilts +Y toward **+Z**, and +Z is forward — so the base angle had to be negative. It is also yawed 0.45 rad to one side now so it clears the cape hem instead of clipping through it.
  - **Everything rendered pale cream.** Not the materials — exposure. Diffuse reached ~1.4× albedo, and per-channel tone-map roll-off desaturates as it compresses. Fixed by cutting the rigs and restoring chroma after the tone map.
  - **Lathe normals inverted** on the pedestal: profiles must run bottom → top or the derived normals point inward.
  - **Rapier mounted across the forearm**, so a thrust pointed the blade at the sky. Now in line with the arm.
- **Next:** gear is still only a proposal; GM sign-off on the Uncommon ancestry; page one above the Skills box still blank; ask the party who has Medicine.

## 2026-08-11

- **Did:** Started the Pathfinder 2e Remaster campaign workspace. Reviewed the existing folder (5e `S.S. Crush` site + the two blank Remaster PDFs Earl added). Created `Pathfinder 2e/` with a README, the character build file, and verbatim Remaster reference for the Rogue class and Catfolk ancestry. Built the level 1 character end to end, then reconciled it against two photos from the table — a whiteboard of Earl's actual picks (IMG_4322) and a partially-filled paper sheet (IMG_4323).
- **Decisions:**
  - Character is **Catfolk Rogue · Scoundrel · Hunting Catfolk · Bounty Hunter**, key attribute **Dexterity** (confirmed from the whiteboard's boost tallies: Dex got 4, only possible as class key).
  - Attributes **Str 14 / Dex 18 / Con 14 / Int 10 / Wis 8 / Cha 14** — verified legal against the Bounty Hunter Str-or-Wis restriction and the all-different rule on free boosts.
  - Feats as Earl chose: Cat's Luck, Nimble Dodge, Lie to Me, plus Experienced Tracker free from background.
  - **Nature** taken as the 7th free trained skill, closing the build at 12 of 12. Medicine deliberately passed over — same +2 modifier, and the only argument for it (Treat Wounds requires trained) depends on whether anyone else in the party covers it.
- **Found:** The paper sheet had **11 trained skills marked against an entitlement of 12** — one free pick unspent. Verified at full resolution across all 18 skill rows, and falsification-tested (Int isn't below 10; Scoundrel grants 2; Bounty Hunter grants 2).
- **Corrected mid-session** — four claims I made that turned out wrong, all now fixed in the character file:
  1. Wrote about a **sap** as though Earl had chosen it; it was my own gear suggestion. No gear is decided.
  2. Argued Medicine was needed to stop a knocked-out mark bleeding out. **Wrong** — nonlethal damage skips the dying condition entirely (*Player Core* p. 410).
  3. Listed the **sap at +7**; it's agile but not finesse, so it attacks off Strength (**+5**). Replaced with **Monkey's Fist** — same price and damage die, but finesse.
  4. Argued Nature was the wrong knowledge domain for a bounty hunter. **Wrong** — Nature covers animals, beasts, fey, plants *and* terrain/weather, which is the broadest low-level monster ID plus the tracker's own domain.
- **Learned (method):** AoN list pages don't render in the in-app browser — query `elasticsearch.aonprd.com/aon/_search` instead and drop hits with a non-empty `remaster_id` to exclude legacy duplicates. HEIC photos need `sips` conversion; crop with PIL, not `sips -c`.
- **Next:** Name the character · choose gear · tick Nature and fill page one above the Skills box · ask the party who has Medicine · GM sign-off on Uncommon Catfolk. PDF fill deferred at Earl's request.
