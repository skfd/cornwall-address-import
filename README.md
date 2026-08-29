# cornwall-address-import

The **Cornwall city checkout** of the address-import family — city #5,
scaffolded 2026-08-15 by the breadth-first onboarding loop (engine
`future-work/multi-city/onboarding-queue.md`). Status: **onboarding**. No
proposal published, no uploads made; the config is a first draft for
conflation baseline runs.

The pipeline lives in the engine repo,
[`address-importer-friend`](https://github.com/skfd/address-importer-friend)
(see its README for setup). This repo carries only Cornwall's `config.toml`,
credentials (`.env.*`, gitignored, from the `.example` files), and — locally,
gitignored — `data/` with the OSM extract and `data/cornwall/tool.db`.

```bash
cd ../address-importer-friend
python run.py --city-dir ../cornwall-address-import
```

Source data: City of Cornwall address points via the sibling
[`ontario-address-changes`](https://github.com/skfd/ontario-address-changes)
tracker (`data/cornwall/cornwall.db`, 20,641 active rows / 17,612 civic
addresses at snapshot 25, 2026-08-15). The 2026-08-12 portfolio survey put
the gap at 14,871 missing (81.1%) — overstated, because Cornwall's
abbreviated suffixes (AV/CR/BV/WY, 32% of rows) were missing from the
normalizer until 2026-08-15; expect the first baseline to come in lower.

Distinctive traits (details in config comments): first city to project its
street from props (`STREET_LNG` — the canonical `street` is the bare name
component); ALL-CAPS streets (title-cased on export since 2026-08-29,
`[export] street_case`); the `full` column prefixes units onto the number ("A-1108 SECOND ST
W"); tiles use the 8 election polling zones at 100% coverage because no
neighbourhood fabric exists — the tile names are polling venues, quirky but
navigable, and freely rebuildable pre-announcement. Cornwall is a separated
city inside SDG county (the Guelph/Wellington containment shape).

Entry state probed 2026-08-15 (`onboarding/entry-state-2026-08-15.json`):
CanVec 7.0 seed (1,127 of 1,365 sampled) plus Matthew Darwin's 2018 rename
retag — but **NOT plain greenfield: `TheRandomGamrTRG` is actively adding
addresses from Cornwall's own open data** (changeset 182902244, 2026-05-19,
3,073 changes, source = the city's ArcGIS portal; 2026 holds 13% of sampled
elements). Untagged as an import, no wiki page — an informal, live, local
effort. **Status: PARKED, contact-first** (the Oakville rule): talk to
TheRandomGamrTRG before running anything visible; offer the tooling, don't
compete. DannyMcD (2019 road-name expansion sweeps) is the second local
contact; Matthew Darwin the third.

Before any production upload: wiki proposal page, forum announcement, and
feedback window per the
[OSM Import Guidelines](https://wiki.openstreetmap.org/wiki/Import/Guidelines)
— Toronto's [`IMPORT_PROPOSAL.mediawiki`](https://github.com/skfd/toronto-2-address-import/blob/main/IMPORT_PROPOSAL.mediawiki)
is the template.

MIT licensed.
