# PhysicalEarth

**The interactive physical atlas the internet is missing.**

Google Maps tells you where the nearest pizza place is. PhysicalEarth tells you *why the world looks the way it does*.

PhysicalEarth is an open-source interactive map viewer that combines hypsometric relief (elevation-based coloring), shaded terrain, ocean bathymetry, geological overlays, and OpenStreetMap detail — the kind of physical geography map you remember from a good school atlas, but zoomable, layered, and alive.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)

## Why?

Every digital map today is optimized for navigation: finding addresses, calculating routes, locating businesses. But the classic physical atlas — with its green lowlands fading to brown highlands, blue ocean depths, and prominent rivers — served a completely different purpose: **understanding geography**.

Why do countries have the borders they have? Why did trade routes go where they went? Why do 3 billion people depend on Himalayan glaciers? A good physical map answers these questions at a glance.

That map doesn't exist online. The data to build it is freely available. The rendering technology is mature. PhysicalEarth brings it all together.

## What it does

- **Hypsometric relief**: GPU-rendered elevation-based colors from green lowlands to white peaks, using an 18-point color ramp inspired by classic atlas aesthetics
- **Hillshade**: 3D terrain shading with northwest illumination for natural depth perception
- **Bathymetry**: Ocean depth visualization from EMODnet — see continental shelves, mid-ocean ridges, and deep trenches
- **OpenStreetMap overlay**: Toggle labels, roads, borders, and detail with adjustable transparency
- **Geological layers**: Overlays from national geological surveys:
  - Spain (IGME, 1:1M)
  - France (BRGM, 1:1M)
  - United Kingdom (BGS, 625K Bedrock)
  - Canada (NRCan, compilation)
- **Layer controls**: Adjust transparency of each layer independently via a collapsible panel

## Quick start

Just open `index.html` in your browser. No build step, no dependencies to install, no server required.

Or visit the live version at [GitHub Pages](https://jorgemelis.github.io/physicalearth/).

## Technology

- **MapLibre GL JS 5.19** — GPU-accelerated map rendering with `color-relief` layer support
- **Zero dependencies** — single HTML file, no npm, no build tools, no frameworks
- All external libraries loaded from CDN

## Data sources and attribution

| Source | Data | License |
|--------|------|---------|
| [Mapterhorn](https://mapterhorn.com/) | DEM elevation tiles (Terrarium encoding) | Free |
| [EMODnet](https://emodnet.ec.europa.eu/) | Bathymetry (ocean depth) | Free with attribution |
| [OpenStreetMap](https://www.openstreetmap.org/) | Base map tiles | ODbL |
| [IGME](https://www.igme.es/) | Geological cartography of Spain (1:1M) | Free with attribution |
| [BRGM](https://www.brgm.fr/) | Geological cartography of France (1:1M) | Free with attribution |
| [BGS/UKRI](https://www.bgs.ac.uk/) | Bedrock geology of the UK (625K) | Free with attribution |
| [NRCan](https://natural-resources.canada.ca/) | Geological compilation of Canada | Free with attribution |
| [Natural Earth](https://www.naturalearthdata.com/) | Rivers (10m) | Public domain |

## Roadmap

### Done
- [x] MapLibre GL JS viewer with GPU-rendered hypsometric tints
- [x] 18-point color ramp (ocean depths to alpine peaks)
- [x] Hillshade with adjustable exaggeration
- [x] EMODnet bathymetry layer
- [x] OpenStreetMap overlay with opacity control
- [x] Collapsible layer control panel with per-layer opacity
- [x] Geological overlays: Spain, France, UK, Canada
- [x] Responsive design with mobile toggle
- [x] Live coordinates display
- [x] Rivers layer with labeled, importance-scaled rendering (Natural Earth 10m)
- [x] GitHub Pages deployment

### Planned
- [ ] Geological legends (WMS GetLegendGraphic)
- [ ] Additional geological surveys (Germany, Italy, USGS, OneGeology)
- [ ] Tectonic plate boundaries
- [ ] Mountain range / peak labels (optional atlas overlay)
- [ ] Climate zones layer
- [ ] Custom label styling (atlas-quality typography)
- [ ] Historical map overlays
- [ ] Fix IGME CORS issue (Spain geology)

## Contributing

We'd love your help! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

Whether you're a cartographer, a GIS developer, a designer, or just someone who loves maps — there's something here for you. Check the Issues tab for tasks labeled `good first issue`.

**Particularly wanted:**
- Cartographic designers who can improve the hypsometric color ramp
- GIS developers familiar with MapLibre styling
- Anyone who can help integrate WMS services from additional national geological surveys
- Feedback on what layers and features would be most useful

## Philosophy

This project is inspired by the work of [Tom Patterson](https://www.shadedrelief.com/) (US National Park Service, retired), whose maps demonstrate that digital cartography can match the beauty and clarity of the best hand-drawn atlases. His [Natural Earth](https://www.naturalearthdata.com/) dataset and cross-blended hypsometric tints are foundational to this project.

The goal is not to replace Google Maps or OpenStreetMap. It's to build the atlas that sits *on top* of them — the layer that turns geographic data into geographic understanding.

## License

MIT License. See [LICENSE](LICENSE).

Data sources retain their own licenses — see the attribution table above.
