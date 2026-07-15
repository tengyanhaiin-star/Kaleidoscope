# Triangular Tessellation Kaleidoscope

A single-file, browser-based kaleidoscope built with HTML5 Canvas. A field of colored particles is reflected across a triangular tessellation to produce a symmetric, ever-shifting pattern — optionally driven by the beat of your own music.

## Features

- **Triangular tessellation rendering** — a seed triangle's content is propagated across a full triangular grid using reflection transforms, so the whole canvas stays perfectly symmetric no matter how the particles move.
- **Particle motion** — a cloud of glowing, colored particles drifts and bounces within a circular boundary, continuously reshaping the pattern.
- **Rotation** — the entire kaleidoscope can spin continuously around its center, independent of particle motion.
- **Adjustable particle size** — five presets (Giant, Large, Medium, Small, Micro) trade off pattern density vs. rendering cost.
- **Audio-reactive visuals** — load any local audio file and the kaleidoscope reacts to it in real time:
  - Particle drift speed and color-cycling speed increase with audio intensity.
  - Particle size pulses with the beat.
  - Rotation speed responds to the music's energy.
- **Volume control** and play/pause for the loaded track.
- **One-click reset** to generate a brand-new random pattern and color palette.

## Usage

1. Open `kaleidoscope_2d_music.html` in a browser — no build step or server required.
2. Use the controls above the canvas:
   - **🔀 Reset** — generate a new pattern.
   - **▶ Start Motion** — animate the particles.
   - **🔄 Start Rotation** — spin the whole pattern.
   - **Particle size dropdown** — switch between Giant/Large/Medium/Small/Micro particles.
   - **📁 Load Music** — pick an audio file from your device to drive the visuals.
   - **▶ Play / Volume slider** — control playback of the loaded track.

## How it works

- A small **source canvas** renders the raw particle field each frame.
- A **seed triangle** is mapped onto that source canvas, then a breadth-first search walks the triangular grid, reflecting the transform across each shared edge so every triangle gets its own affine mapping back into the source content.
- Each frame, every triangle in the grid is clipped and painted with the (transformed) source canvas onto an **offscreen canvas**, which is then drawn onto the visible canvas — rotated, if rotation is active.
- The offscreen canvas is sized just large enough to cover the circle the visible area can sweep through while rotating, keeping the triangle count (and per-frame clipping cost) as low as possible.
- Audio analysis uses the Web Audio API's `AnalyserNode` to read frequency data each frame; the average amplitude drives particle speed, color-cycle speed, particle scale, and rotation speed.

## Tech stack

- Vanilla JavaScript, HTML5 Canvas 2D — no external libraries.
- Web Audio API for audio-reactive analysis and playback.
- [Inter](https://fonts.google.com/specimen/Inter) (via Google Fonts) for UI typography.

## Browser support

Works in any modern browser with Canvas 2D and Web Audio API support (Chrome, Firefox, Safari, Edge).
