# Earthtone

**Listen to Earth.** Earthtone turns NASA satellite imagery into orchestral music in the browser. Move the map anywhere on the planet and a small synthesized orchestra plays what it sees.

Live demo: https://eenessreal.github.io/earthtone/

Built for the **NASA Space Apps Challenge 2026**, challenge *The Earth Information Jukebox*, by team **Earthtone**.

## How it works

A playhead sweeps across the current map view from left to right. The view is split into 48 vertical bands, and each band becomes one eighth note.

| Image feature | Musical result |
|---|---|
| Brightness of the band | Melody pitch (brighter = higher) |
| Dominant surface: water / vegetation / bare land / cloud & ice | Instrument: flute / violins / bright violins / celesta |
| Color saturation | Note volume |
| Surface change (coastline, cloud edge) | Harp strum |
| Variety and color of the next 8 bands | Arrangement size: strings only → harp, basses, timpani, second violin line |

Underneath, a string section plays a chord progression (I–V–vi–IV in major, i–VI–III–VII in minor). Melody notes on strong beats snap to the current chord, and large jumps are folded back by an octave, so any landscape is heard as a tune rather than noise.

## NASA data

- **NASA GIBS (Global Imagery Browse Services)** WMTS tiles, EPSG:3857:
  - Blue Marble: Shaded Relief and Bathymetry
  - MODIS Terra Corrected Reflectance (True Color), daily, user-selectable date
  - VIIRS Black Marble night lights (2016)
  - Reference labels (for orientation only; not used for sound)

## Tech

- Plain HTML, CSS and JavaScript, no build step
- [Leaflet](https://leafletjs.com/) for the map
- Web Audio API for all sound: Karplus-Strong plucked strings (harp), detuned sawtooth strings with vibrato, FM celesta, flute with breath noise, synthesized timpani and cymbal swell, convolution reverb
- Hosted on GitHub Pages

## Use of AI

Claude (Anthropic) was used as a coding assistant to help write and debug the JavaScript and the sound engine, and to help draft this README. The concept, musical direction (instrument choices, chord progressions, arrangement) and testing were done by the team. No AI-generated images, audio or video are included in the app; all sound is synthesized live in the browser.

## Run locally

Open `index.html` in a browser, or serve the folder with any static server.
