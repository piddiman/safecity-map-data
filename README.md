# SafeCity map data

Washrooms, drinking water, pharmacies and road speed limits in British Columbia, for the SafeCity iPhone app. A weekly job
rebuilds these files from OpenStreetMap; each build replaces the last one.

- `v2/manifest.json`: when it was built, the tile size, and how many places each tile has
- `v2/washrooms/<tile>.json`: public washrooms, and chains, stores, malls, libraries and community centres that
  have one, in one tile of 0.25 by 0.5 degrees (about 28 x 36 km). A tile is named `<row>_<column>`: the floor of
  latitude / 0.25 and longitude / 0.5, e.g. `196_-246` for Surrey.
- `v2/essentials/<tile>.json`: drinking water and pharmacies (most BC pharmacies give out free naloxone kits)
- `v2/speeds/<tile>.json`: roads with a posted speed limit, as lines: `{"type": "way", "id", "tags", "g"}`, where
  `g` is the road's points as `[lat, lon, lat, lon, ...]` and `tags` keeps `maxspeed` (and `:forward`/`:backward`),
  `highway`, `name` and `oneway`. A road crossing tiles is in each of them.
- `v2/lanes/<tile>.json`: roads whose lanes are marked with the way each goes, as lines like the speed limits, with
  `turn:lanes` (or `:forward`/`:backward`), `highway` and `oneway`, for lane guidance before a turn. Highway exits
  with no lanes marked get them worked out from the lane counts at the split (four lanes becoming three beside a
  one-lane ramp: the right lane exits), tagged `source:turn:lanes=lane_count`; marked lanes always win
- `v2/hours/<tile>.json`: chains' own opening hours from All the Places, `{"stores": [{"brand", "lat", "lon",
  "hours"}]}`, for places people add from Apple Maps (which shares no hours)
- `v1/`: Metro Vancouver in one file per dataset, for app versions from before tiles

The files use the Overpass API's JSON shape: `{"elements": [{"type", "id", "lat", "lon", "tags"}]}`.

Where OpenStreetMap has no opening hours for a chain's location, the hours of the same store from
[All the Places](https://www.alltheplaces.xyz) (the chains' own store finders, released under CC-0) fill the
gap; those places carry `source:opening_hours=alltheplaces`. `atp-stores.json.gz` keeps the province's stores
from All the Places, so a week when it can't be reached builds from the last copy instead.

Data © [OpenStreetMap contributors](https://www.openstreetmap.org/copyright), available under the
[Open Database License](https://opendatacommons.org/licenses/odbl/). These files are a derived database
under the same licence. Hours from All the Places: CC-0.
