# MOG Wildlife Identification Dashboard

A single-page, tabbed HTML dashboard for identifying 11 groups of North American mammals from
camera-trap photos, using range maps, an iNaturalist presence check, and Mature and Old-Growth
Forest Mammal Project (MOG) 2025 camera-trap detections. This is a direct structural duplicate
of the Snapshot USA Wildlife Identification Dashboard, with the camera-trap layer swapped for
the MOG project's own data.

## Groups / tabs

Cervidae (Odocoileus, Cervus, Alces, Rangifer), Sylvilagus, Lepus, Neotoma, Sciurus, Glaucomys,
Ammospermophilus, Urocitellus, Ictidomys, Otospermophilus, Xerospermophilus.

## Data sources

- **IUCN Red List range polygons**, **iNaturalist Research-grade presence grid**, species
  palettes, identification tips, and taxonomy reconciliation against MDD v2.5 -- all identical
  to the Snapshot USA dashboard build (same 14 genera, same continental-US + Alaska scope, same
  taxonomy decisions and data gaps; see that project's README for full detail on those layers).
- **MOG 2025 camera-trap detections** -- Wildlife Insights sequence-level data from the Mature
  and Old-Growth Forest Mammal Project (Herrera, Kays, McMurry, Cove; NC Museum of Natural
  Sciences), aggregated to the subproject level (mean lat/lon across deployments), shown as
  large squares split into equal-width color stripes by number of distinct species/categories
  detected there. 224 deployments across 11 subprojects, concentrated in Southwestern US
  mature/old-growth forests (Gila NF, Kaibab, Carson NF, Moab/Manti-La Sal, Spring Mountain,
  Hoosier NF, Cibola NF).

## MOG-specific data notes

- **Deployment repair**: 10 deployments had a null `subproject_name` but their `placename`
  field literally read `LowerMLS_Moab_XX`, and their coordinates fell within the same tight
  geographic cluster as the 11 deployments already labeled `Moab`. Reassigned to the `Moab`
  subproject for consistent aggregation, following the same repair pattern used on the
  Snapshot Brazil dashboard's RebioPerobas deployments.
- **Genera with zero MOG detections**: Neotoma, Ammospermophilus, Urocitellus, Ictidomys, and
  Xerospermophilus were not detected anywhere in this dataset -- their range and iNaturalist
  grid layers still display normally on those tabs, just with an empty camera-trap layer. This
  reflects MOG's forest-focused deployment strategy rather than a data or pipeline error.
- **No new taxonomy work required**: every species MOG detected (Odocoileus hemionus/
  virginianus, Cervus canadensis, Sciurus aberti/carolinensis/niger, Lepus americanus/
  californicus/townsendii, Otospermophilus variegatus, Sylvilagus audubonii/floridanus/
  nuttallii, Glaucomys volans) was already resolved and covered in the Snapshot USA
  dashboard's palette and identification-tips data.
- **"Emperor Penguin"**: the MOG dataset tags 665 detections (concentrated in New Mexico and
  Arizona forest deployments) with the species name *Aptenodytes forsteri* -- the ID team's
  internal shorthand for "clearly a mammal, no idea which one," not an actual penguin sighting.
  The dashboard's banner explains this so it doesn't read as a data error on first glance.

## Files

- `mog_dashboard.html` -- the dashboard, self-contained with all data embedded, validated
  end-to-end in a headless DOM (jsdom + Leaflet + Turf) test across all 11 tabs.

## Design notes

Identical to the Snapshot USA dashboard: only one range source (IUCN or iNaturalist) shown at
a time, hover shows all overlapping species names, no cross-species overlap/richness layer.
