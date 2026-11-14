# Earthtone

**Listen to Earth.** Earthtone turns NASA satellite imagery into orchestral music in the browser. Move the map anywhere on the planet and a small synthesized orchestra plays what it sees.

Live demo: https://eenessreal.github.io/earthtone/

Built for the **NASA Space Apps Challenge 2026**, challenge *The Earth Information Jukebox*, by team **Earthtone**.

## How it works

Each view is heard in two layers.

**1. The landscape picks the piece.** The whole view is read as one scene. Each kind of scene has its own tempo, rhythm of the tune, accompaniment figure, pad and a live synthesized soundscape.

| Scene | Piece and soundscape |
|---|---|
| Mostly ocean | *Open ocean*: slow, rolling harp, choir; surf and gulls |
| Land and sea | *Coast*: harp, light timpani; light surf and gulls |
| Bare land, no sea | *Desert*: oud, ney with grace notes, soft drone, frame drum; desert wind |
| Vegetation in the tropics | *Rainforest*: marimba, pan flute, tribal drums; insects, frogs, exotic birds, rain |
| Vegetation elsewhere | *Green lands*: pizzicato strings, violins, horns; birdsong and a stream |
| Cloud or ice | *Ice and cloud*: glass harmonica, celesta, choir; cold wind, cracking ice |
| Grey built-up areas (daily MODIS layer) | *City*: driving strings, brass, drum kit; traffic, crowd murmur, horns, sirens |
| Night lights layer | *City lights* or *Night*; crickets in the dark |

**2. The location picks the local sound.** The map centre decides the scale and the instruments, so the same kind of landscape sounds different around the world.

| Region | Scale | Instruments and local details |
|---|---|---|
| Egypt, Sahara & Arabia | Double harmonic | Qanun, ney, strings in unison, frame drum, finger cymbals |
| Anatolia (incl. Istanbul) | Makam Hicaz | Bağlama, ney, soft darbuka; Bosphorus ferry horns and gulls in the city |
| Aegean | Kürdi | Bouzouki tremolo, kaval, guitar, def |
| Japan | In (miyako-bushi) | Koto, shakuhachi, taiko; temple bells, Tokyo crossing signals |
| China & Southeast Asia | Gong pentatonic | Guzheng with glissandi, erhu, dizi, gongs, woodblocks |
| India | Raag Khamaj | Sitar with meend, bansuri, tanpura drone, tabla |
| Sub-Saharan Africa | Major pentatonic | Kalimba, djembe |
| Australia | (landscape's own) | Didgeridoo, clapsticks |
| Andes | Minor pentatonic | Quena, pan flute, charango, bombo |
| Brazil (coast and cities) | Major with 7th chords | Bossa nova guitar, flute, samba percussion |
| Celtic isles | D Mixolydian | Tin whistle, fiddle, harp, bodhrán, pipe drones |
| Mexico | Major | Mariachi trumpets, violins, vihuela |
| Central Asian steppe | Minor pentatonic | Dombra, galloping rhythm, overtone singing, bowed fiddle |
| Elsewhere | (landscape's own) | Western orchestra |

When the map moves into a different kind of place, the music changes piece at the next bar with a cymbal and timpani (or gong) transition.

Then a playhead sweeps across the current map view from left to right. The view is split into 48 vertical bands, and each band becomes one eighth note.

| Image feature | Musical result |
|---|---|
| Brightness of the band | Melody pitch (brighter = higher) |
| Dominant surface: water / vegetation / bare land / cloud & ice | Instrument: flute / violins / bright violins / celesta |
| Color saturation | Note volume |
| Surface change (coastline, cloud edge) | Harp strum |
| Variety and color of the next 8 bands | Arrangement size: strings only → harp, basses, timpani, second violin line |

Underneath, a string section plays the mood's chord progression (for example E–F–E–D in Desert, Dmaj7–E–Dmaj7–A in Ocean). Melody notes on strong beats snap to the current chord, and large jumps are folded back by an octave, so any landscape is heard as a tune rather than noise.

## Features

- **World tour**: one tap flies the map through deserts, coasts, cities at night, rainforests, the open ocean and ice, and the music changes piece at every stop.
- **Explore by touch**: drag a finger (or use the arrow keys) over the view to hear the spot underneath. Each surface has its own instrument and brighter places sound higher, so people who cannot see the image can still explore Earth by ear. A live text line announces the surface for screen readers.
- **Share this place**: the link keeps the exact view, layer and date (`#lat,lng,zoom,layer[,date]`).
- **My location**: flies to where you are, so you can hear your own region.
- **Save 30 s clip**: renders the current view offline at full quality and returns a WAV file.

## Listening on a phone

- Notes are scheduled about 0.3 s ahead on the audio clock, so a busy device does not break the rhythm.
- **Sound engine: Light** (default on touch devices) uses block-rate modulation, a shorter mono reverb and fewer layers.
- **Save 30 s clip** renders the current view offline at full quality with an `OfflineAudioContext` and returns a WAV file, so the result never stutters, whatever the device.

## NASA data

- **NASA GIBS (Global Imagery Browse Services)** WMTS tiles, EPSG:3857:
  - Blue Marble: Shaded Relief and Bathymetry
  - MODIS Terra Corrected Reflectance (True Color), daily, user-selectable date
  - VIIRS Black Marble night lights (2016)
  - Reference labels (for orientation only; not used for sound)
- **Science data layers** that change the music (shown as a coloured overlay):

| Layer | GIBS product | What it does to the music |
|---|---|---|
| Sea surface temperature | GHRSST L4 MUR SST | Warm seas: faster, bright glass shimmer. Cold seas: slower, low choir breath |
| Land surface temperature | MODIS Terra LST (day) | Heat makes the music faster and brighter |
| Active fires | VIIRS / MODIS thermal anomalies | Crackles under the playhead, dark brass swell and timpani roll |
| Rain | IMERG precipitation rate | Rain soundscape, slower tempo, thunder in heavy rain |
| Vegetation | MODIS NDVI (8-day) | More birdsong where vegetation is denser |

The colour of each data pixel is read back into a value (for temperature, its position on the blue-to-red scale; for fires and rain, how much of each column they cover). Layer names and zoom levels are checked at run time; a product that is not available switches itself off and the music plays without it.

## Tech

- Plain HTML, CSS and JavaScript, no build step
- [Leaflet](https://leafletjs.com/) for the map
- Web Audio API for all sound: Karplus-Strong plucked strings (harp), detuned sawtooth strings with vibrato, FM celesta, flute with breath noise, synthesized timpani and cymbal swell, convolution reverb
- Hosted on GitHub Pages

## Use of AI

Claude (Anthropic) was used as a coding assistant to help write and debug the JavaScript and the sound engine, and to help draft this README. The concept, musical direction (instrument choices, chord progressions, arrangement) and testing were done by the team. No AI-generated images, audio or video are included in the app; all sound is synthesized live in the browser.

## Run locally

Open `index.html` in a browser, or serve the folder with any static server.
