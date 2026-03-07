# PhysicalEarth - Claude Code Instructions

## Project Overview
GPU-rendered interactive hypsometric atlas. Single-file web app (`index.html`) using MapLibre GL JS 5.19. No build tools, no frameworks, no npm.

## Conceptual Model
The **relief** is this project's core contribution — hypsometric tints, bathymetry, and hillshade are always present as the foundation. On top of the relief, users can optionally enable a **reference layer** (Satellite or OpenStreetMap) for orientation or educational purposes. All other overlays (rivers, geology, atlas labels) sit on top of everything.

## Architecture
Everything lives in `index.html` (~800 lines):
- HTML: map container + control panel UI
- CSS: glass-morphism styling, geology group styles
- JS: map init, layer management, UI interactivity

## Key Technical Details
- **MapLibre GL JS 5.19** loaded from CDN (unpkg)
- **color-relief** layer type for hypsometric tints (GPU-rendered)
- **Terrarium encoding** DEM tiles from Mapterhorn (512px)
- **Reference layers**: Esri World Imagery (satellite) and OpenStreetMap, controlled by a unified selector with shared opacity
- **WMS layers** for geology via `addGeologyWMS()` helper function
- **GeoJSON rivers** from Natural Earth 10m with zoom-dependent filtering
- **Glyphs**: `https://protomaps.github.io/basemaps-assets/fonts/{fontstack}/{range}.pbf` (Noto Sans Regular/Medium/Italic)
- Layer order: hypsometric → bathymetry → hillshade → satellite → OSM → geology → rivers (line + label)
- Default view: Europe centered [10, 40], zoom 4

## Default Layer State
| Layer | ON/OFF | Opacity |
|-------|--------|---------|
| Hypsometric Tints | ON | 100% |
| Bathymetry | ON | 100% |
| Hillshade | ON | 35% |
| Reference layer (Satellite/OSM) | Satellite selected | 50% |
| Rivers | ON | 100% |
| Minor Rivers | OFF | 100% |
| Atlas Labels | OFF | 100% |
| Geology (all) | OFF | 50% |

## UI Details
- Panel opens expanded by default
- Reference layer selector (Satellite / OSM) at top of layers list with shared opacity slider (always visible); opacity 0% effectively hides the reference layer, so no "None" button is needed
- Geology layers grouped under single "Geology" heading with individual country toggles
- Rivers toggle controls both line and label layers simultaneously

## Data Sources
| Source | URL | Type |
|--------|-----|------|
| Mapterhorn | tiles.mapterhorn.com | DEM (terrarium) |
| Esri World Imagery | server.arcgisonline.com | Raster tiles (satellite reference) |
| EMODnet | tiles.emodnet-bathymetry.eu | Raster tiles |
| OpenStreetMap | tile.openstreetmap.org | Raster tiles (OSM reference) |
| Natural Earth | raw.githubusercontent.com/nvkelso/natural-earth-vector | GeoJSON (rivers 10m, marine 10m, mountains 10m, peaks 10m) |
| IGME (Spain) | mapas.igme.es | WMS |
| BRGM (France) | geoservices.brgm.fr | WMS |
| BGS (UK) | ogc.bgs.ac.uk | WMS |
| NRCan (Canada) | maps-cartes.services.geo.ca | WMS |
| SPW (Belgium/Wallonia) | geoservices.wallonie.be | WMS |
| DOV (Belgium/Flanders) | www.dov.vlaanderen.be | WMS |
| LNEG (Portugal) | sig.lneg.pt | WMS |

## Development Guidelines
- Keep the single-file architecture: no build tools, no splitting into modules
- All dependencies from CDN
- New layers should be optional and toggleable with opacity controls
- Test by opening `index.html` in a browser
- Maintain the glass-morphism UI style
- Geology layers default to OFF (visibility: 'none')
- Follow existing patterns: `addGeologyWMS()` for new WMS layers, `setupLayerControl()` for UI bindings
- Rivers use a custom control (toggle controls both line + label layers)
- Seas & Oceans layer uses Natural Earth 10m marine polygons with Spanish name fallback (`name_es` → `name`)

## Deployment
- GitHub Pages from `main` branch
- Repository: github.com/jorgemelis/physicalearth
- Just push to main — no build step needed

## Known Issues
- Spain geology (IGME): CORS issues — may not load in browser
- Hillshade opacity slider controls `hillshade-exaggeration`, not `hillshade-opacity`
- Rivers dataset (Natural Earth 10m) has ~1,455 rivers — smaller national rivers (e.g. Júcar) may not be included
- Atlas Labels: Natural Earth 10m only has 222 mountain ranges worldwide. Coverage is uneven — well-covered areas (Central Europe, Himalayas, Andes) vs gaps (Spain has only Cantábrica, Sierra Nevada, Sierra Morena; missing Sistema Central, Ibérico, Bética, Costero-Catalana, Montes de Toledo). Contributions welcome: add missing ranges to a custom GeoJSON overlay or submit to [Natural Earth](https://github.com/nvkelso/natural-earth-vector)

## Next Steps (Priority Order)

### 1. Geological Legends (partially done)
Implemented: Canada (NRCan), France (BRGM). Click to open full-size in independent window.
Remaining:
- **UK (BGS)**: 499x1720px — needs scrollable container
- **Spain (IGME)**: 822x2286px — needs scrollable container, use GetLegendGraphic URL

### 3. Morocco Geology Layer (BLOCKED)
- **Source**: XYZ tiles at `cartesgeoscientifiques.mem.gov.ma/data/fgl/{z}/{x}/{y}.png`
- **Issue**: Server sends duplicate `Access-Control-Allow-Origin: *` header — browsers reject it
- **Status**: Tiles are valid (verified via curl) but unusable from browser until server is fixed

### 4. Future Ideas
- Additional geological surveys (Germany, Italy, USGS)
- Tectonic plate boundaries
- Climate zones
- OpenFreeMap vector tiles for higher-zoom labels (z8+)
