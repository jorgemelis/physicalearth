# PhysicalEarth - Claude Code Instructions

## Project Overview
GPU-rendered interactive hypsometric atlas. Single-file web app (`index.html`) using MapLibre GL JS 5.19. No build tools, no frameworks, no npm.

## Architecture
Everything lives in `index.html` (~800 lines):
- HTML: map container + control panel UI
- CSS: glass-morphism styling, geology group styles
- JS: map init, layer management, UI interactivity

## Key Technical Details
- **MapLibre GL JS 5.19** loaded from CDN (unpkg)
- **color-relief** layer type for hypsometric tints (GPU-rendered)
- **Terrarium encoding** DEM tiles from Mapterhorn (512px)
- **WMS layers** for geology via `addGeologyWMS()` helper function
- **GeoJSON rivers** from Natural Earth 10m with zoom-dependent filtering
- **Glyphs**: `https://protomaps.github.io/basemaps-assets/fonts/{fontstack}/{range}.pbf` (Noto Sans Regular/Medium/Italic)
- Layer order: hypsometric → bathymetry → hillshade → OSM → geology → rivers (line + label)
- Default view: Europe centered [10, 40], zoom 4

## Default Layer State
| Layer | ON/OFF | Opacity |
|-------|--------|---------|
| Hypsometric Tints | ON | 100% |
| Bathymetry | ON | 100% |
| Hillshade | ON | 35% |
| OpenStreetMap | ON | 0% (slider visible, user can increase) |
| Rivers | ON | 100% |
| Geology (all) | OFF | 50% |

## UI Details
- Panel opens expanded by default
- OSM layer-body starts open (slider immediately visible)
- Geology layers grouped under single "Geology" heading with individual country toggles
- Rivers toggle controls both line and label layers simultaneously

## Data Sources
| Source | URL | Type |
|--------|-----|------|
| Mapterhorn | tiles.mapterhorn.com | DEM (terrarium) |
| EMODnet | tiles.emodnet-bathymetry.eu | Raster tiles |
| OpenStreetMap | tile.openstreetmap.org | Raster tiles |
| Natural Earth | raw.githubusercontent.com/nvkelso/natural-earth-vector | GeoJSON (rivers 10m) |
| IGME (Spain) | mapas.igme.es | WMS |
| BRGM (France) | geoservices.brgm.fr | WMS |
| BGS (UK) | ogc.bgs.ac.uk | WMS |
| NRCan (Canada) | maps-cartes.services.geo.ca | WMS |

## Development Guidelines
- Keep the single-file architecture: no build tools, no splitting into modules
- All dependencies from CDN
- New layers should be optional and toggleable with opacity controls
- Test by opening `index.html` in a browser
- Maintain the glass-morphism UI style
- Geology layers default to OFF (visibility: 'none')
- Follow existing patterns: `addGeologyWMS()` for new WMS layers, `setupLayerControl()` for UI bindings
- Rivers use a custom control (toggle controls both line + label layers)

## Deployment
- GitHub Pages from `main` branch
- Repository: github.com/jorgemelis/physicalearth
- Just push to main — no build step needed

## Known Issues
- Spain geology (IGME): CORS issues — may not load in browser
- Hillshade opacity slider controls `hillshade-exaggeration`, not `hillshade-opacity`
- Geological legends NOT yet implemented (see next section)
- Rivers dataset (Natural Earth 10m) has ~1,455 rivers — smaller national rivers (e.g. Júcar) may not be included

## Next Steps (Priority Order)

### 1. Geological Legends
Legend images via `<img>` tags (NOT fetch — avoids CORS issues):
- **Canada (NRCan)**: 150x612px, 12KB — trivial, just works
- **UK (BGS)**: 499x1720px — needs scrollable container
- **Spain (IGME)**: 822x2286px — needs scrollable container, use GetLegendGraphic URL
- **France (BRGM)**: Dynamic legend is 10,014px tall (unusable). Use static JPG: `https://mapsref.brgm.fr/legendes/geoservices/Geologie1000_legende.jpg` (600x732)

Implementation: add `<img loading="lazy">` inside geology group. Wrap in scrollable div.

### 2. Atlas Labels (mountains, seas, peaks) — OPTIONAL toggle, OFF by default
Use Natural Earth GeoJSON datasets:
- `ne_50m_geography_regions_polys.geojson` — mountain ranges, deserts, plains
- `ne_10m_geography_regions_elevation_points.geojson` — peaks with elevation
- `ne_50m_geography_marine_polys.geojson` — oceans, seas, bays
Atlas conventions: UPPERCASE brown for mountains, italic blue for water.

### 3. Future Ideas
- Additional geological surveys (Germany, Italy, USGS)
- Tectonic plate boundaries
- Climate zones
- OpenFreeMap vector tiles for higher-zoom labels (z8+)
