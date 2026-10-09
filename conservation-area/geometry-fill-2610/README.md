# Conservation-area geometry fills, October 2026

888 conservation-area entities on the Planning Data Platform have no geometry. Each one comes from an MHCLG
(`government-organisation:D1342`) file in `digital-land/conservation-area-data` (`data/Output/Missing/` or
`data/Output/ExistingMismatched/241216/`). That repository was archived on 7 August 2026, so these files are here.
None of the entities is in an LPA that sends its own conservation-area data (checked 9 October 2026).

- `<PREFIX>-conservation-area.csv` (64 files): one row for each entity:
  - `reference`: the reference in the entity's MHCLG file. The existing D1342 lookups map it to the entity.
  - `entity`: for people. The conservation-area pipeline ignores this column (`column.csv` maps it to IGNORE).
  - `geometry`: WKT, WGS84.

  `<PREFIX>` is the prefix of the entity's MHCLG file. So the nightly MHCLG retire rule ends a fill file at the same
  time as that file, when the LPA starts to send its own data.
- `sources.csv`: where each polygon came from: source URL, publisher, provenance class and the licence notes of the
  research. The PDP does not collect this file.

Sources: 877 polygons were downloaded from public bodies' GIS services (LPAs, counties, national park authorities,
Historic England, the GLA). 11 West Northamptonshire polygons were traced from the council's PDF boundary maps with
the Extract set-up (extract-alpha #801): 2 runs each, the runs agree at IoU 0.947 to 0.999, and a person checked the
overlays against the council maps.

These files hold only the geometry, so they change no other field. The existing MHCLG files were not changed,
because a changed file gives every fact in it a new entry-date, and older MHCLG values would then replace newer
Historic England values on 272 rows.
