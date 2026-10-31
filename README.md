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
- `v1/`: Metro Vancouver in one file per dataset, for app versions from before tiles

The files use the Overpass API's JSON shape: `{"elements": [{"type", "id", "lat", "lon", "tags"}]}`.

Data © [OpenStreetMap contributors](https://www.openstreetmap.org/copyright), available under the
[Open Database License](https://opendatacommons.org/licenses/odbl/). These files are a derived database
under the same licence.
