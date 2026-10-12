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
- `sources.csv`: where each polygon came from, one row for each entity. The PDP does not collect this file.
  - `source-url`, `method` (`download`, or `extract` for a polygon traced from a PDF), `publisher`.
  - `provenance-class` (A to D) and `provenance-class-meaning`: who publishes the source and whether the LPA links
    to it. `lpa-link` and `lpa-link-meaning`: the strongest link that was proved. `lpa-link-page`: the LPA page with
    that link. `publisher-link-page`: the publisher's page that links to the source (for another public body).
  - `licence-stated`, `licence-scope` (`dataset`, `site`, `notice-only`, `restrictive` or `none`), `licence-use` and
    `licence-use-meaning` (`ok`, `check`, `ask` or `blocked`: what the stated terms allow), `licence-url` (the page or
    record that states the licence), `data-gov-uk-url`, `licence-statement` (quoted), `attribution`, `licence-notes`
    (what was checked) and `licence-checked-on`.
  - 79 rows (Devon, Rugby, Chesterfield, Guildford) have no `licence-url`: no licence statement was found for those
    sources. `licence-notes` says where the research looked.

Sources: 877 polygons were downloaded from public bodies' GIS services (LPAs, counties, national park authorities,
Historic England, the GLA). 11 West Northamptonshire polygons were traced from the council's PDF boundary maps with
the Extract set-up (extract-alpha #801): 2 runs each, the runs agree at IoU 0.947 to 0.999.

These files hold only the geometry, so they change no other field. The existing MHCLG files were not changed,
because a changed file gives every fact in it a new entry-date, and older MHCLG values would then replace newer
Historic England values on 272 rows.
