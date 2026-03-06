# Generative Brand System — FLOWERS

A prototype exploring **runtime brand rendering**: brand identity as a generative grammar rather than static assets.

## Concept

The brand "FLOWERS" has:
- **Invariants**: wordmark typography, composition rules, spatial relationships
- **Variables**: a generative flower element that changes based on context (location, season, etc.)

Each location maps to a native flower species (roses in India, tulips in Netherlands, sakura in Japan...) rendered procedurally within brand constraints. Every instance is unique but recognizably the same brand.

## Run

Open `index.html` in a browser. No server needed.

## Structure

- `index.html` — Self-contained single-file app (HTML + CSS + JS)
- Procedural flower generation via Canvas API
- Seeded PRNG for reproducible variants
- Location-to-flower mapping with parametric variation
