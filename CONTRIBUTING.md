# Contributing to PhysicalEarth

Thank you for your interest in contributing! PhysicalEarth aims to be the interactive physical atlas the internet is missing, and we need help from cartographers, developers, designers, and geography enthusiasts alike.

## How to contribute

### Reporting issues
- Use GitHub Issues for bug reports and feature requests
- For feature requests, describe the use case: why would this layer or feature help people understand geography?
- Screenshots and map comparisons are always welcome

### Code contributions
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improved-color-ramp`)
3. Make your changes
4. Test by opening `index.html` in a browser
5. Commit with clear messages
6. Push to your fork and open a Pull Request

### What we especially need

**Cartographic design**
- Improving the hypsometric color ramp to match classic atlas aesthetics
- Better color transitions between elevation zones
- Typography choices for geographic labels
- Visual hierarchy for different feature types

**GIS / Data integration**
- Adding WMS layers from national geological surveys
- Integrating bathymetric data
- Processing and optimizing tile sources
- Adding vector layers (tectonic plates, climate zones, etc.)

**Documentation**
- Translating the README (Spanish, French, German especially welcome)
- Writing guides for adding new WMS data sources
- Documenting the cartographic choices and why they were made

## Technical guidelines

- Keep it simple: no build tools, no frameworks, no npm. Just HTML, CSS, and JavaScript.
- The viewer must work by opening index.html in any modern browser.
- External libraries are loaded from CDNs (MapLibre GL JS).
- New layers should be optional and toggleable.
- Respect data source licenses and attribution requirements.

## Code of conduct

Be kind, be constructive, be patient. This is a project built by people who love maps and want to share that with the world.

## Questions?

Open an issue or start a discussion. There are no stupid questions, especially about cartography.
