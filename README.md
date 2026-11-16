# Earth Jukebox

**The ocean as an orchestra.** NASA Space Apps Challenge 2026, challenge: *The Earth Information Jukebox*.
Team **It Depends**: Erina Maeda-Makrelova, Chiyu Oshima, Hayeon Bang, Tigran Misakyan.

Earth Jukebox turns NASA ocean visualizations into music. Point at the ocean, sweep a scan across it, steer with hand gestures or your voice, or ride a western boundary current from the tropics toward the pole, and hear temperature and currents played by an orchestra. NASA shows Earth science almost entirely through color, which leaves out anyone who cannot read a color bar. We wanted to know whether an orchestra can let listeners hear where the ocean is warm or cold, and how its currents flow, without relying on color.

**Try it:** https://hayeonwhale.github.io/NasaSpaceX_earth-jukebox/ (Chrome or Edge recommended)
**Demo slides:** [docs/demo](https://hayeonwhale.github.io/NasaSpaceX_earth-jukebox/docs/demo/) (7 slides, also as a [PDF](docs/Earth-Jukebox-Project-Demo.pdf)) · **Submission text:** [SUBMISSION.md](SUBMISSION.md)

![Earth Jukebox tracing the Gulf Stream on NASA's Perpetual Ocean 2 video](docs/screenshot.jpg)

## How the data becomes music

| On the map | In your ears |
|---|---|
| Temperature | Pitch: warmer water sounds higher, and notes snap to the chord being played so the music stays in key. Cold water plays **piano**; warm water plays **brass** (trumpet, horn, trombone), blending between about 8 and 24 °C. Temperature is the most prominent part of the music. |
| Current strength | **Strings** (violin, viola, cello). A stronger current makes them louder and fuller, with deeper, faster vibrato and tremolo. The strings stay audible but secondary. |
| Current steadiness | Steady flow sounds smooth and joined; uneven flow sounds short and detached. |
| Current direction | East or west moves the sound between your ears. North or south steps the melody up or down one chord note. |

Real instrument samples (FluidR3 General MIDI, through WebAudioFont) load with the first map; built-in synthesized instruments take over if they cannot load. Only the strings vibrate, so the piano and brass stay in tune, and every note is kept within its instrument's comfortable range.

## Ways to explore

- **Load** a NASA animation (drop in the video), or use the built-in sample map, the boundary-currents map, or the boundary-currents video.
- **Point** with the mouse, a finger on a touch screen, the arrow keys, or your hand on camera. The music follows that spot as the video plays.
- **Scan** sweeps the visible map in any direction and plays one note per strip.
- **Zoom and pan** with the wheel, the buttons, + and −, or by dragging. The music then describes only what you can see, and *Where am I?* names the ocean, sea or current.
- **Hand control** (MediaPipe; camera video stays on your computer):

  | Gesture | Action |
  |---|---|
  | One finger | Point at a place and hear it |
  | Two fingers | Zoom in |
  | Three fingers | Zoom out |
  | Four fingers | Swipe to scan in that direction |
  | Five fingers | Say where you are (point with one finger first) |
  | Two fists | Stop |
  | One fist | Turn on voice control |

- **Voice control**: “go to the Gulf Stream”, “zoom in”, “scan left”, “where am I”, “trace the Kuroshio”, “boundary currents tour”, “stop”, “reset the map”.
- **Saved maps**: save the current view with a title and description in your browser, and reopen it later.
- Every reading appears in a live status line for screen readers and can be spoken aloud.

## Western boundary currents

These are narrow, fast, warm currents pressed against the west side of every ocean basin by Earth's rotation, and they carry tropical heat toward the poles. NASA's [Perpetual Ocean 2: Western Boundary Currents](https://svs.gsfc.nasa.gov/5425/) (SVS 5425, one of the challenge resources) shows them as a 3D camera flight, which cannot be read as a map. Earth Jukebox uses the same ECCO2 model run in its flat, equirectangular form ([SVS 5479](https://svs.gsfc.nasa.gov/5479/)).

- **Five currents:** Gulf Stream, Kuroshio, Agulhas, Brazil and East Australian. Their paths are approximate long-term core positions, checked against the NASA frames. They are drawn as dashed lines whose dashes drift with the flow.
- **Ride one:** the view glides to the current and the cursor rides along its core while the music reads the real map underneath it. The direction of the path sets the stereo position and the melody steps. As the water cools on its way toward the pole, the pitch falls and piano takes over from brass. For example, the Gulf Stream reads about 21 °C off Florida and about 13 °C out in the Atlantic, and the Agulhas about 15 °C along Africa and about 9 °C where it turns back.
- **Tour:** Kuroshio, then Agulhas, then the Gulf Stream (the order of NASA's film), each with a short spoken introduction.
- **Reading NASA's colors:** Perpetual Ocean 2 draws see-through trails on a navy ocean. Each pixel is therefore split into “trail color × opacity + navy”, and the best-fitting stop on the 0–25 °C color bar gives the temperature. Bright trails count more than faint dark ones, so the music follows what you see. A 0.25° land mask, built from three frames a year apart (land never moves), stops beige deserts from being read as warm water.

## NASA data

- **Global Sea Surface Currents and Temperature**, NASA Scientific Visualization Studio ([SVS 3912](https://svs.gsfc.nasa.gov/3912/)): the main map and the built-in sample. Temperature is color on a 0–32 °C color bar; currents are the moving streaks.
- **Perpetual Ocean 2** (ECCO2 model, 2022–2023): the flat temperature version ([SVS 5479](https://svs.gsfc.nasa.gov/5479/)) is the boundary-currents map and video, and [SVS 5425](https://svs.gsfc.nasa.gov/5425/) is the reference for the tour and the color bar. The video in `media/` is re-encoded to H.264 (38 MB), because NASA's server does not allow other websites to read its video pixels.
- **ECCO:** Estimating the Circulation and Climate of the Ocean (NASA JPL and MIT).

Visualizations: NASA's Scientific Visualization Studio.

## References and AI use

- Walker, B. N., & Nees, M. A. (2011). Theory of sonification. In T. Hermann, A. Hunt, & J. G. Neuhoff (Eds.), *The Sonification Handbook*. Logos Verlag Berlin.
- Code and write-up were drafted with AI assistance (Claude). The team chose the idea, the audience, the sound mappings and the controls.

## Limits and next steps

This is a working prototype, and listening tests are still to come. We make no claims for blind users until blind and low-vision listeners have tried it. Next we want to test four questions:

- Can listeners tell which of two regions is warmer by sound alone?
- Do fuller, more vibrant strings and choppier notes read as a stronger, less steady current?
- Can flow direction be learned from stereo position and scale steps, on headphones?
- Can a user reach a place, zoom in and hear its reading with gestures and voice only?

## Run it

Use the live site, or serve this folder:

```
python3 -m http.server 8000
```

Then open http://localhost:8000. Opening `index.html` straight from disk also works, except the *Boundary-currents video* button: browsers will not let a page opened from a file read a video beside it. In that case choose `media/perpetual-ocean-2-temperature.mp4` with *Choose a map*. Voice control needs a browser with speech recognition (Chrome or Edge). Instrument samples (WebAudioFont) and the hand tracker (MediaPipe) load from the internet.

## Built with

One HTML file and no build step: Canvas 2D, the Web Audio API with WebAudioFont, MediaPipe Hand Landmarker, and the Web Speech API (recognition and synthesis).
