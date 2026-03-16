# 911 EMS Coverage Map - Project State

## What This Is
Interactive map showing which agency provides 911 EMS ambulance transport for every area.
Goal: Fill a gap that no one has built - a public-facing map of "who runs 911 EMS here?"

## Current State (2026-03-16)

### Colorado (index.html)
- 108 agencies researched, all 64 counties covered (63 with known providers, Jackson County unknown)
- County-level polygons colored by provider type
- City-level detail for ~80 cities overlaid on top
- Dark basemap, search bar, county/city toggle, click-to-zoom legend

### Georgia (georgia.html)
- 134 agencies researched, all 159 counties covered (157 with known providers, Glascock & Taliaferro unknown)
- County-level polygons colored by provider type
- Athens-Clarke County: 71 fire district sub-zones (10 stations) from ACC GIS overlaid
- Athens city limits shown as dashed yellow outline
- UGA School of Law marker at 225 Herty Drive (33.9480, -83.3773) with red UGA-branded label
- 30+ city boundaries for Athens area + major GA cities (Atlanta, Savannah, Augusta, etc.)
- Athens area: National EMS (Priority Ambulance) covers Clarke, Oconee, Morgan. County EMS covers others.
- Major statewide: Grady EMS (~17 rural south GA counties), Priority Ambulance (~20 counties), AMR (DeKalb, N. Fulton), MetroAtlanta Ambulance (Cobb, Bartow, Paulding)
- Zoom buttons: UGA Law, Athens, Athens Region, Atlanta Metro, Statewide
- Default view: Athens at zoom 12
- GA has no statewide fire district GIS data (unlike CO). EMS is county-based.

## Site Structure
- **index.html** - US landing page with clickable state map
- **colorado.html** - Colorado with real fire district boundaries (267 districts)
- **georgia.html** - Georgia counties + Athens fire districts + UGA Law marker
- **contribute.html** - Report errors / submit state data (wiki-style)

## Files
```
ems-911-map/
  index.html                          - US landing page with clickable state map
  colorado.html                       - Colorado state map
  georgia.html                        - Georgia state map
  contribute.html                     - Error reporting / state submission page
  data/
    colorado-statewide.json           - 108 agencies with coverage, type, confidence, sources
    co-state.geojson                  - Colorado state boundary (Census TIGER)
    co-counties.geojson               - All 64 county boundaries (Census TIGER)
    co-places.geojson                 - 484 city/CDP boundaries (Census TIGER)
    boundaries.geojson                - [OLD] 31 Denver metro city boundaries
    counties.geojson                  - [OLD] 8 Denver metro county boundaries
    denver-metro.json                 - [OLD] 16 Denver metro agencies
    georgia-statewide.json            - 134 GA agencies with coverage, type, confidence
    ga-state.geojson                  - Georgia state boundary (Census TIGER)
    ga-counties.geojson               - All 159 GA county boundaries (Census TIGER)
    ga-places.geojson                 - 538 GA city/CDP boundaries (Census TIGER)
```

## Tech Stack
- Leaflet.js (CDN) for map rendering
- CARTO dark basemap tiles
- Census TIGER GeoJSON for boundaries
- Vanilla JS, no build tools, runs on localhost via `python3 -m http.server 8090`

## How It Works
1. County polygons render as base layer, colored by provider type
2. City polygons overlay when zoomed in (>= zoom 10) or "Cities" view selected
3. Color scheme: teal = third service/gov, red = fire dept, yellow = private, gray = mixed
4. Search works for city or agency names
5. Legend items clickable to zoom

## Data Sources
- CDPHE ground ambulance licensing
- RETAC regional provider lists (all 10 RETACs)
- 5280Fire.com agency database
- Individual agency websites
- Denver Metro EMS Medical Directors member list
- Census TIGERweb REST API for boundaries

## Known Gaps / TODO
- Jackson County provider unknown
- Colorado Springs AMR contract status uncertain post-April 2025
- Many small rural volunteer FDs not mapped (BLS first response, not transport)
- Fire district boundaries != city boundaries (fire districts are the real coverage units)
- Need to validate Denver metro with local knowledge (Jaden knows the area)
- Need Arvada to show on map (it's in data but may need the place boundary)

## Next Steps Discussed
- Georgia (Athens area) next state to map
- Consider scraping job postings as a data source
- Eventually: all 50 states
- Could become a product/tool for EMS job seekers

## Running Locally
```bash
cd ~/Desktop/Entrepreneurship/Other/ems-911-map
python3 -m http.server 8090
# then open http://localhost:8090
```
