# SUPERSPACE — Castaway of Oru

A retro side-scrolling platformer you play with **hand gestures** through your phone's camera.
One file (`index.html`), no build step, no image or sound files — the pixel art and the music are drawn and synthesised in code.

Built so far: the gesture controls, calibration, the gesture test screen, the title screen, and
**Desert 1 – Dune Sea** with its boss, Mawra the Dune Worm. The other seven courses are listed in the
course select as "SOON"; worlds, courses, enemies and bosses are data-driven so they can be added later.

## Play it

1. Host `index.html` on any **HTTPS** address (the camera only works on a secure address).
   On GitHub: merge this branch into `main`, then *Settings → Pages → Deploy from a branch → `main` / root*.
2. Open the page on your phone in Safari or Chrome, turn the phone sideways, prop it up with the
   front camera facing your hands (1–2 feet away), and screen-mirror it to a TV.
3. Tap **PLAY WITH CAMERA**, allow the camera, then follow the hand setup screen.

On a computer, choose **KEYBOARD ONLY**: arrow keys run, Space jumps (again in the air to double jump),
X spins, Esc/P pauses, M mutes, F toggles full screen. On a phone without the camera you get touch buttons.

## Gestures

| Hand | Gesture | Does |
| --- | --- | --- |
| Action | Finger-walk (index + middle finger alternating like legs) | Run — faster wiggle, faster run |
| Action | Open palm | Jump |
| Action | Open palm → close → open palm, in the air | Double jump |
| Action | Fist | Spin attack |
| Direction | Fast swipe left / right | Face that way |
| Direction | Fast swipe while the hero is in the air (or just before a jump) | Air push — shoves the hero that way through the air |

The hero keeps running for about 0.4 s after you stop finger-walking, and keeps that speed through a jump.
From a standstill (for example, stopped against a block) a jump goes straight up — swipe the direction hand to push the hero over.
The game pauses by itself when your hands leave the frame. In menus, swipe to move and hold an open palm to select.
**Options → Easy run** lets you run by simply holding two fingers out.

## Tuning

Everything you are likely to tweak is in the `TUNE` object at the top of the script in `index.html`:

- `TUNE.gesture` — gesture thresholds (the Gesture Test screen has live sliders for the main ones)
- `TUNE.feel` — forgiveness: run-on time, coyote time, input buffers, ledge assist
- `TUNE.hero` — speed, jump height, spin timing
- `TUNE.difficulty` — lives, health, invincibility time, enemy and boss speed, hazard strength

Enemy numbers live in `ENEMIES`, boss numbers (per tier) in `BOSSES`, and the level maps in `COURSES`.

## If hand tracking misbehaves

Hand tracking is MediaPipe Gesture Recognizer, loaded from a CDN and run entirely on the device
(in a Web Worker where the browser allows it, so the game stays smooth). The Gesture Test screen shows
the tracking rate. These address options can help when troubleshooting:

- `?tracker=main` — run the tracker on the main thread instead of a worker
- `?frames=pixels` — send camera frames to the worker as copied pixels
- `?cpu=1` — never use the GPU for tracking
