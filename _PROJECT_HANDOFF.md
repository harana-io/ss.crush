# D&D / Pathfinder 2e — Project Handoff

**Last updated:** 2026-08-11
**Status:** PF2e Remaster character build is mechanically complete at level 1. All 12 trained skills assigned, all level 1 feats chosen, attributes locked and verified legal. Outstanding: **gear** (proposal only), GM sign-off on the Uncommon ancestry, and transcribing everything above the Skills box onto the paper sheet.

---

## Goal & scope

Build and maintain Earl's player character for a new **Pathfinder Second Edition (Remaster)** campaign, and keep accurate rules reference alongside it.

**In scope:** the character build, rules reference, filling the official character sheet.
**Out of scope (so far):** GM material, campaign setting, party composition. The 5e `S.S. Crush/` and `earl-animation/` folders are the previous campaign — leave them alone.

---

## The character

**Catfolk Rogue · Scoundrel racket · Hunting Catfolk heritage · Bounty Hunter background · Level 1**
Key attribute: **Dexterity**. Name: **Cat the Bounty Hunter**.

*Concept:* a catfolk manhunter who works the talking side of the job — imprecise scent at 30 ft, tracking at a dead run, and a Feint that leaves the mark off-guard for the rapier.

| Str | Dex | Con | Int | Wis | Cha |
|---|---|---|---|---|---|
| 14 (+2) | **18 (+4)** | 14 (+2) | 10 (+0) | 8 (−1) | 14 (+2) |

**AC 18** · **HP 18** · Perception **+4** · Fort **+5** · Reflex **+9** · Will **+4** · Class DC **17** · Speed **25 ft**
Proficiency boxes at level 1: trained = **3**, expert = **5** (Perception, Reflex, and Will are all expert).

**Level 1 feats:** Cat's Luck (ancestry) · Nimble Dodge (class) · Lie to Me (skill) · Experienced Tracker (background, free)

**All 12 trained skills:** Acrobatics +7, Stealth +7, Thievery +7, Athletics +5, Deception +5, Diplomacy +5, Intimidation +5, Performance +5, Legal Lore +3, Society +3, Nature +2, Survival +2

Full detail, including the levels 2–5 plan and page-one fill values, is in `Pathfinder 2e/Character - Catfolk Scoundrel Rogue.md`.

---

## How it's built / where things live

```
D&D/
├── _START_HERE.md · _PROJECT_HANDOFF.md · _SESSION_LOG.md
├── Pathfinder 2e/
│   ├── README.md                                  hub
│   ├── Character - Catfolk Scoundrel Rogue.md     THE deliverable
│   ├── Reference/  Rogue.md · Catfolk.md          verbatim Remaster rules
│   ├── character-sheet.html                       interactive sheet: dice, HP, sneak attack
│   └── character-3d.html                          WebGL model: posable, fight clips
├── RemasterPlayerCoreCharacterSheet*.pdf          blank sheets
├── IMG_4322.heic  IMG_4323.HEIC                   whiteboard + paper sheet photos
└── S.S. Crush/ · earl-animation/                  previous 5e campaign — don't touch
```

### Rules sourcing — use the AoN Elasticsearch backend

Archives of Nethys list pages render via JS that **does not fire** in the in-app browser, so scraping them returns empty results. Query the open backend directly instead:

```
POST https://elasticsearch.aonprd.com/aon/_search
```

- Filter on `category`: `feat` · `heritage` · `ancestry` · `racket` · `background` · `equipment` · `weapon` · `armor` · `skill` · `class` · `rules` · `action` · `skill-general-action`
- **Drop any hit with a non-empty `remaster_id`** — that field marks the *legacy* pre-Remaster duplicate of the same entry. Every rule in this project was filtered this way.
- Useful fields: `text`, `trait`, `level`, `price_raw`, `bulk_raw`, `damage`, `primary_source_raw`, `rarity`

A helper lives in the scratchpad as `aon.py` (`q(body)` → dict). Recreate it if the scratchpad is gone; it's ~8 lines of `urllib`.

### Reading the table photos

- HEIC won't open directly: `sips -s format png IMG_4322.heic --out out.png`
- **Crop with PIL, not `sips -c`** — `--cropOffset` doesn't crop from the top-left as expected and silently returns a centered band.
- The whiteboard tally marks are **attribute boosts**, not modifiers. They sum to exactly 10, which is the level 1 allowance — that's how the key attribute was confirmed as Dexterity.

---

## Decisions & rationale

| Decision | Why |
|---|---|
| **Dexterity as key attribute** | Dex received 4 boosts, only possible with Dex as class key. Charisma would have bought +1–2 on Feint at the cost of attack, AC, Reflex, Class DC, and the three best skills. |
| **Str 14 / Wis 8** (rather than Str 12 / Wis 10) | The Scoundrel racket does **not** add Dex to damage — that's the *Thief* racket. Strength is the only damage modifier, so Str 14 is +2 per Strike. Perception drops to +4, which matters little since Surprise Attack wants Stealth (+7) rolled for initiative anyway. |
| **Nature as the 7th free skill** | Covers Recall Knowledge on animals, beasts, fey, plants — the creature types that dominate low levels — plus geography, weather, environment. Pairs with Survival: Survival does the *doing*, Nature the *knowing*. The marks themselves are humanoids → Society, already trained. |
| **Medicine deliberately skipped** | Same +2 modifier as Nature, no math tiebreaker. Treat Wounds *requires trained* (unlocks a capability) whereas Recall Knowledge works untrained (Nature merely improves it) — so Medicine wins **only if nobody else in the party has it**. Unresolved; see Next Steps. |
| **Leather armor over studded leather** | Both reach AC 18 at Dex 18, but studded caps Dex at +3 and gets worse as Dex rises. Leather's Strength requirement is +0, so at Str 14 there's **no armor check penalty**. |
| **Monkey's Fist over Sap** | Both 1 sp, both 1d6 B nonlethal. The sap is *agile* but **not finesse**, so it attacks off Strength (+5). Monkey's Fist **is** finesse → +7. Both carry sneak attack. |

---

## Guardrails & conventions

- **Remaster terminology only.** *off-guard* (not flat-footed) · *Thieves' Toolkit* (not thieves' tools) · *attribute* (not ability score) · *Player Core* / *Player Core 2* (not CRB / APG).
- **Verify before asserting.** Several confident claims turned out wrong this session (see the log). Query AoN rather than answering from memory, especially on trait interactions and skill/creature-type mappings.
- **Don't attribute proposals to Earl.** Gear in the character file is a *suggestion*; the only things Earl has actually chosen are on the whiteboard.
- **Git: ask before committing.** Everything is untracked on `main`. The remote (`harana-io/ss.crush`) is named for the old 5e campaign, which is confusing but correct.

---

## Key rules facts worth not re-deriving

- **Nonlethal damage never causes dying.** *Player Core* p. 410 — a target dropped by a nonlethal attack is simply **unconscious at 0 HP**, no dying condition, nothing to stabilize. Any weapon can strike nonlethally at a **−2 circumstance penalty** (p. 407); weapons with the nonlethal trait skip it.
- **Finesse ≠ agile.** Only *finesse* lets you attack with Dexterity; *agile* only reduces the multiple-attack penalty. Either trait qualifies a weapon for sneak attack.
- **Rogue's 7 + Int free skills is the highest in the game** — every other class gets 2–4. Total entitlement here: Stealth (class) + 2 (racket) + 2 (background) + 7 free = **12**.
- **Recall Knowledge mapping** (*Player Core* p. 231): Nature → animals, beasts, fey, plants, terrain, weather · Society → humanoids, personalities, legal institutions · Religion → undead, fiends, celestials · Occultism → aberrations, spirits, oozes · Arcana → constructs, beasts, elementals.
- **Catfolk is Uncommon** even in *Player Core 2* — needs GM access.
- The **fillable PDF has 517 auto-generated field names** (`text_15gujr`, `checkbox_44scmk`) with no semantic labels. Filling it programmatically requires mapping fields by page position against the printed labels.

---

## Open items / Next steps

- [ ] **Choose gear.** Nothing is decided; the character file has a 12 gp 3 sp proposal (leather, rapier, Monkey's Fist, 3 daggers, shortbow, Thieves' Toolkit, Adventurer's Pack) out of 15 gp.
- [ ] **Tick Nature on the paper sheet** — T checked, `3` in the Prof box.
- [ ] **Fill page one above the Skills box** — it's entirely blank. Exact values are in the character file's "Filling the Rest of Page One" section.
- [ ] **Ask the party who has Medicine.** If nobody does, that's the hole to cover — though the level 2 skill increase is otherwise earmarked for Deception (expert, +7).
- [ ] **Get GM sign-off on Catfolk** (Uncommon ancestry).
- [ ] **Optional: fill the form-fillable PDF.** Deferred by Earl — "markdown now, fill later."
