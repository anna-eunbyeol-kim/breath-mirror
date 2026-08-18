<img width="1736" height="385" alt="fogether" src="https://github.com/user-attachments/assets/15feb602-e2b2-431b-8c46-7f64e700fe24" />

# Fogether

A browser-based **foggy glass you share with someone far away**. Open your mouth to fog it up, wipe it clear with your hand (or a finger on your phone), and leave little marks for your partner to find. No install, single HTML file.

It began as a solo "breath mirror", now it's a long-distance thing for two. *(fog + together)*

## How it works

Both of you open the same page and type the **same room name** (or one shares an invite link). Now you're looking at the same pane of glass:

- **Open your mouth** : like breathing on cold glass, the mirror fogs over. When your partner breathes, *your* glass fogs too, with a soft ripple where they blew. No microphone, so talking never triggers it. (Works for everyone in frame, up to 4 faces.)
- **Wipe it clear** : **pinch** your thumb and index finger and move (on a computer), or **drag your finger** across the screen (on a phone). Draw a heart, write a word, or just clear a peek-hole. Your partner sees your hand move as a soft warm glow.
- **✎ Leave a mark** : fog up, draw something, then tap *leave mark*. Your partner receives it — even the *last second of you drawing it*, like a Live Photo. It's kept even if they're offline, and the last 5 are archived (browse with ‹ ›).
- **Photo** : both hands in an **"L"**, held ~1.5s → a 3·2·1 selfie, saved to the strip at the bottom and shared to both of you.
- **↩ undo / ✕ clear** : undo the last wipe, or clear the glass (synced to both).

You can **start alone** and invite your partner anytime — the badge shows your room name and copies an invite link. When they arrive it turns to *"💙 here together,"* and their breath, wipes, and marks appear on your glass in real time.

## Running it locally

Needs camera access (no microphone), which browsers only grant over `localhost` or HTTPS. Opening the file directly (`file://`) is unreliable — serve it:

```bash
cd fogether
python3 -m http.server 8080
```

Then open `http://localhost:8080/` in Chrome (best MediaPipe support) and allow the camera.

## Deploying (to use it long-distance)

It's a single `index.html`, drop it on any static host over HTTPS and both people open that URL. This one runs on [Vercel](https://vercel.com): push to the repo and it deploys automatically.

## Setup notes

- **Landing image** : put a `landing.jpg` next to `index.html` for the entrance background (a warm gradient shows otherwise). It gets the frosted-glass + cursor-wipe effect automatically.
- **Offline notes** *(optional)* : marks always sync live over P2P and save on your device. To have them delivered even when you two aren't online at the same time, set `FIREBASE_DB_URL` in `index.html` to a free [Firebase Realtime Database](https://firebase.google.com/docs/database) URL (with rules restricting writes to `/notes/$room`). Leave it empty and notes still work live + on-device.
- **Font** : the landing title uses [Unbounded](https://fonts.google.com/specimen/Unbounded).

## How it's built

Single `index.html`, everything from CDNs, no build step:

- [MediaPipe Hands](https://github.com/google-ai-edge/mediapipe) — pinch to wipe, L-shape for photos
- MediaPipe Face Mesh, open-mouth breath detection (no mic)
- [Trystero](https://github.com/dmotz/trystero) — serverless peer-to-peer rooms (same room name = connected, no signaling server to run)
- Firebase Realtime Database — optional offline note delivery

## Credits

Grown from a reference "breath mirror" hand-tracking demo, turned into a shared glass for two.
