# Breath Mirror

A browser-based "mirror" that fogs up when you open your mouth to blow on it, and clears with your hands — no install, single HTML file, powered by [MediaPipe Hands](https://github.com/google-ai-edge/mediapipe) for hand tracking and MediaPipe Face Mesh for open-mouth detection.

## Gestures

- **Open your mouth (as if blowing)** — face tracking detects the open mouth and fogs up the mirror. Works for everyone in frame at once (up to 4 faces), and no microphone is used, so talking/ambient noise never triggers it. The fog fades away on its own about a minute after the last breath.
- **Pinch (thumb + index finger)** — wipe a clear circle through the fog.
- **Both hands in an L-shape**, held for 1.5s — starts a 3-2-1 countdown and takes a photo (saved to the photo strip at the bottom; hover a thumbnail to download it).
- **↩ undo / ✕ clear** buttons — undo the last wipe, or clear everything immediately.

## Running it

This needs camera access (no microphone), which browsers only grant on a "secure context." Opening the file directly (`file://`) works in some browsers but is unreliable — serving it over `localhost` is the reliable way:

```bash
cd ~/projects/breath-mirror
python3 -m http.server 8080
```

Then open `http://localhost:8080/` in Chrome (best MediaPipe/WebRTC support) and allow camera access when prompted.

## Credits

Adapted from a reference "breath mirror" hand-tracking demo, with open-mouth (face tracking) breath detection in place of a microphone.
