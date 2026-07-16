![Uploading Screenshot 2026-07-15 at 10.03.42 AM.png…]()
# Breath Mirror

A browser-based "mirror" that fogs up when you breathe on it, and clears with your hands — no install, single HTML file, powered by [MediaPipe Hands](https://github.com/google-ai-edge/mediapipe) for hand tracking and the Web Audio API for breath detection.

## Gestures

- **Blow on the screen** — the mic picks up breath noise and fogs up the mirror.
- **Pinch (thumb + index finger)** — wipe a clear circle through the fog.
- **Make a fist** (hold ~0.2s) — instantly clear all the fog, like a windshield wipe.
- **Both hands in an L-shape**, held for 1.5s — starts a 3-2-1 countdown and takes a photo (saved to the photo strip at the bottom; hover a thumbnail to download it).
- **↩ undo / ✕ clear** buttons — undo the last wipe/fist-clear, or clear everything.

## Running it

This needs camera + microphone access, which browsers only grant on a "secure context." Opening the file directly (`file://`) works in some browsers but is unreliable — serving it over `localhost` is the reliable way:

```bash
cd ~/projects/breath-mirror
python3 -m http.server 8080
```

Then open `http://localhost:8080/` in Chrome (best MediaPipe/WebRTC support) and allow camera + microphone access when prompted.

## Credits

Adapted from a reference "breath mirror" hand-tracking demo, with an added fist-to-clear gesture.
