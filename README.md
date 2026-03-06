# Generative Brand Identity

A working prototype for brand identity that changes based on context. Instead of a fixed logo, the brand has rules and constraints that produce different but recognizable expressions depending on where, when, and for whom it appears.

## What this is

The brand "FLOWERS" has two parts:

1. **Fixed elements** - the wordmark typography, composition layout, and spatial rules never change
2. **Variable elements** - the flower illustration changes based on context (location maps to a native species)

The flower acts as a dropcap, replacing the "F" in FLOWERS. Each location gets its own species (lotus for India, sakura for Japan, protea for South Africa, etc.) but the overall mark stays recognizable.

Two rendering modes:
- **Curated** - AI-generated ink illustrations (Gemini 3.1 Flash Image), backgrounds removed with rembg
- **Generative** - procedural flowers rendered live on Canvas with a seeded PRNG, different every time

## Run

Open `index.html` in a browser. No build step, no server needed.

Or serve locally:

```
cd prototypes/Generateivebrand
python3 -m http.server 8877
```

## Files

```
index.html          Single-file app (HTML + CSS + JS)
assets/             AI-generated flower images
  *-nobg.png        Background-removed versions (used in the app)
  *.png             Original generations
NOTES.md            Research notes, references, experiment log
README.md           This file
```

## Locations

India (Lotus), Japan (Sakura), Netherlands (Tulip), England (Rose), Mexico (Marigold), France (Lavender), South Africa (Protea), Hawaii (Hibiscus), Colombia (Orchid), USA (Sunflower)
