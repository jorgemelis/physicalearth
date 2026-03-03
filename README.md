# PhysicalEarth

**The interactive physical atlas the internet is missing.**

Google Maps tells you where the nearest pizza place is. PhysicalEarth tells you *why the world looks the way it does*.

PhysicalEarth is an open-source interactive map viewer that combines hypsometric relief (elevation-based coloring), shaded terrain, and OpenStreetMap detail — the kind of physical geography map you remember from a good school atlas, but zoomable, layered, and alive.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)

## Why?

Every digital map today is optimized for navigation: finding addresses, calculating routes, locating businesses. But the classic physical atlas — with its green lowlands fading to brown highlands, blue ocean depths, and prominent rivers — served a completely different purpose: **understanding geography**.

Why do countries have the borders they have? Why did trade routes go where they went? Why do 3 billion people depend on Himalayan glaciers? A good physical map answers these questions at a glance.

That map doesn't exist online. The data to build it is freely available. The rendering technology is mature. PhysicalEarth brings it all together.

## What it does

- **Hypsometric relief**: Elevation-based colors from green lowlands to white peaks — see terrain at a glance
- **OpenStreetMap overlay**: Toggle OSM labels and detail on top of the relief with adjustable transparency
- **Bathymetry**: Ocean depth visualization (planned)
- **Geological layers**: Optional overlays from geological surveys like IGME (planned)
- **Layer controls**: Adjust transparency of each layer independently

## Quick start

Just open `index.html` in your browser. No build step, no dependencies to install, no server required.

## Data sources and attribution

PhysicalEarth combines open data from multiple sources:

| Source | Data | License |
|--------|------|---------|
| [OpenStreetMap](https://www.openstreetmap.org/) | Vector map data | ODbL |
| [OpenTopoMap](https://opentopomap.org/) | Topographic tiles | CC-BY-SA |
| [Natural Earth](https://www.naturalearthdata.com/) | Physical geography vectors | Public domain |
| [IGME](https://www.igme.es/) | Geological cartography of Spain | Free reuse with attribution |

IGME data attribution: "Origen de los datos: ©CN Instituto Geológico y Minero de España (IGME)"

## Roadmap

### v0.1 — Current
- [x] MapLibre GL JS viewer
- [x] Terrain relief base layer with hillshading
- [x] OpenStreetMap overlay with opacity control
- [x] Layer control panel
- [ ] Basic bathymetry

### v0.2 — Planned
- [ ] Geological overlay layer (IGME WMS for Spain)
- [ ] Improved hypsometric color ramp (cross-blended tints)
- [ ] River prominence scaling
- [ ] Mountain range labels

### v0.3 — Future
- [ ] Additional geological surveys (BGS, BRGM, OneGeology)
- [ ] Tectonic plate boundaries
- [ ] Climate zones layer
- [ ] Historical map overlays
- [ ] Custom label styling (atlas-quality typography)

## Contributing

We'd love your help! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

Whether you're a cartographer, a GIS developer, a designer, or just someone who loves maps — there's something here for you. Check the Issues tab for tasks labeled `good first issue`.

**Particularly wanted:**
- Cartographic designers who can improve the hypsometric color ramp
- GIS developers familiar with MapLibre styling
- Anyone who can help integrate WMS services from national geological surveys
- Feedback on what layers and features would be most useful

## Philosophy

This project is inspired by the work of [Tom Patterson](https://www.shadedrelief.com/) (US National Park Service, retired), whose maps demonstrate that digital cartography can match the beauty and clarity of the best hand-drawn atlases. His [Natural Earth](https://www.naturalearthdata.com/) dataset and cross-blended hypsometric tints are foundational to this project.

The goal is not to replace Google Maps or OpenStreetMap. It's to build the atlas that sits *on top* of them — the layer that turns geographic data into geographic understanding.

## License

MIT License. See [LICENSE](LICENSE).

Data sources retain their own licenses — see the attribution table above.
