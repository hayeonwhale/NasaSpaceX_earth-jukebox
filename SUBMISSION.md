# Space Apps submission text (copy and paste)

Team **It Depends** · Challenge: **The Earth Information Jukebox** · NASA Space Apps Challenge 2026

## Project name

Earth Jukebox: The Ocean as an Orchestra

## High-level summary

Earth Jukebox turns NASA ocean visualizations into music, so ocean temperature and currents can be explored by ear as well as by eye. It reads the colors and motion of NASA's Global Sea Surface Currents and Temperature animation and of Perpetual Ocean 2, live in the browser. Cold water plays piano and warm water plays brass, with pitch rising as the water warms. Currents play strings that grow fuller and vibrate more as the flow strengthens. Steady flow sounds smooth, and the direction of flow moves the sound between your ears. You can point at any place, sweep a scan across the map, or ride a western boundary current such as the Gulf Stream and hear its water cool on the way to the pole. Everything also works with hand gestures and voice commands, and every reading can be spoken aloud. NASA presents Earth science almost entirely through color, which leaves out people who are blind, have low vision or are color blind. We built this to ask whether an orchestra can carry the same information.

## Project demo

- Slides (7): https://hayeonwhale.github.io/NasaSpaceX_earth-jukebox/docs/demo/ (PDF: `docs/Earth-Jukebox-Project-Demo.pdf` in the repository)

## Final project

- Live app: https://hayeonwhale.github.io/NasaSpaceX_earth-jukebox/
- Code: https://github.com/hayeonwhale/NasaSpaceX_earth-jukebox

## Project details

**What it does.** Earth Jukebox is a web page that plays a NASA ocean animation and turns what it shows into an orchestra in real time. Temperature sets the pitch and the instrument family: piano for cold water, brass for warm water, blending between about 8 and 24 °C. Current strength drives a string section that grows louder and fuller, with deeper, faster vibrato and tremolo. Steady currents give long connected notes and fluctuating ones give short detached notes. East–west flow pans the sound, and north–south flow steps the melody up or down. Only the strings vibrate, so temperature stays the most prominent part of the music.

**How it works.** Each frame is drawn to a canvas, and each ocean pixel's color is converted back to a temperature with NASA's own color bar (0–32 °C for the sea-surface map, 0–25 °C for Perpetual Ocean 2). Current strength comes from how much the streaks move between frames, and their direction from block matching. Perpetual Ocean 2 draws see-through trails over a navy ocean, so each pixel is split into “trail color × opacity + navy” before reading it. A land mask, built from three frames a year apart, keeps beige deserts from sounding like warm water.

**Ways to explore.**
- Point with a mouse, touch or the arrow keys.
- Scan the map in any direction, one note per strip.
- Zoom in so the music describes only what is in view.
- Ride one of five western boundary currents (Gulf Stream, Kuroshio, Agulhas, Brazil, East Australian), or take a narrated tour of three.
- Use hand gestures through the webcam (MediaPipe): one finger points, two zoom in, three zoom out, a four-finger swipe scans, five fingers say where you are, two fists stop, one fist starts voice control.
- Use voice commands such as “go to the Gulf Stream” or “trace the Kuroshio”.
- Save maps with a title and description.

**Why it matters.** Sonification opens NASA's Earth visualizations to people who cannot rely on color, and gives everyone a second sense for patterns such as warm boundary currents carrying heat poleward. This is a working prototype, and listening tests with blind and low-vision listeners are the next step. We make no claims for blind users until they have tried it.

**Tools.** HTML, Canvas 2D, the Web Audio API with WebAudioFont (FluidR3 General MIDI samples), MediaPipe Hand Landmarker, and the Web Speech API. It runs entirely in the browser with no install, and camera video never leaves the user's computer.

## NASA data

- Global Sea Surface Currents and Temperature, NASA Scientific Visualization Studio: https://svs.gsfc.nasa.gov/3912/
- Perpetual Ocean 2: Western Boundary Currents (challenge resource): https://svs.gsfc.nasa.gov/5425/
- Perpetual Ocean 2, equirectangular projection (flat map and video used for the boundary currents): https://svs.gsfc.nasa.gov/5479/
- Underlying model: ECCO2, Estimating the Circulation and Climate of the Ocean (NASA JPL and MIT)

## Space agency partner and other data

- No partner-agency data.
- Other resources: WebAudioFont instrument samples (FluidR3 General MIDI), and the MediaPipe Hand Landmarker model.

## References

- Walker, B. N., & Nees, M. A. (2011). Theory of sonification. In T. Hermann, A. Hunt, & J. G. Neuhoff (Eds.), *The Sonification Handbook*. Logos Verlag Berlin.
- NASA Scientific Visualization Studio pages listed above.

## Use of AI

Code and write-up were drafted with AI assistance (Claude, by Anthropic). The team chose the idea, the audience, the sound mappings and the controls, and reviewed and tested the results. No AI-generated images, audio or video are presented as NASA data. All map imagery comes from NASA's Scientific Visualization Studio.
