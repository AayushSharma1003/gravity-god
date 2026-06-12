# gravity god 🌌

![JavaScript](https://img.shields.io/badge/Made%20with-JavaScript-f7df1e?style=for-the-badge&logo=javascript&logoColor=black)
![MediaPipe](https://img.shields.io/badge/MediaPipe-Hands-blue?style=for-the-badge&logo=google&logoColor=white)
![Canvas 2D](https://img.shields.io/badge/Canvas-2D%20Physics-ff6b35?style=for-the-badge)
![No Install](https://img.shields.io/badge/No%20Install-Just%20a%20Browser-27ae60?style=for-the-badge)
![Live](https://img.shields.io/badge/Live-GitHub%20Pages-0366d6?style=for-the-badge&logo=github)

> your webcam becomes a physics universe. your hands are the gravity.

110 glowing particles. real Newtonian physics. your hands control everything.

**[try it live →](https://aayushsharma1003.github.io/gravity-god/)**

---

<!-- drop a screenshot here when you have one -->
<!-- ![gravity god in action](preview.png) -->

---

## what your hands do

| gesture | what happens |
|---|---|
| 🖐 **open palm** | gravity well — everything drifts toward your hand |
| ✊ **fist** | crush — strong field packs matter into a dense core |
| ✊ → 🖐 **fist then open** | supernova — radial shockwave blasts everything outward |
| 🤌 **pinch** | spawn — new matter appears at your fingertips |
| 🖐🖐 **two open palms** | tug-of-war — matter gets torn between both hands |

keyboard: `G` toggles world gravity · `R` resets · `C` clears all matter

---

## how it works

```
webcam feed (30fps)
    ↓
MediaPipe Hands — 21 landmarks per hand
    ↓
gesture classifier (open / fist / pinch)
    ↓
Newtonian force engine
    ├── each particle has: position, velocity, mass, radius
    ├── hand gestures apply inverse-square attraction fields
    ├── fist: extra velocity damping near the core
    └── supernova: one-shot radial impulse on fist → open
    ↓
Canvas 2D renderer
    ├── webcam as mirrored background (cover-fit)
    ├── velocity-based coloring: slow = blue, fast = red/orange
    ├── motion trails (last 9 positions)
    └── additive blending glow pass
    ↓
pairwise collision resolution (positional separation + impulse)
```

every particle interacts with every other one. 110 bodies, 60fps, all in a single HTML file.

---

## running locally

no build step, no dependencies beyond a browser:

```bash
git clone https://github.com/AayushSharma1003/gravity-god.git
cd gravity-god
open index.html   # Chrome works best
```

---

## the physics, actually

each frame, for every particle `b` and every visible hand `h`:

```
force = strength × mass / (distance² + softening)
velocity += force / mass × dt
position += velocity × dt
```

the softening term (`+4000` for open palm, `+2500` for fist) prevents the singularity you'd get at zero distance and keeps the simulation stable. fist gets extra velocity damping near the hand so matter physically compresses into a core instead of just orbiting forever.

the supernova is a single one-shot impulse applied to every particle within `blastRadius` pixels — scaled by `(1 - distance / blastRadius)` so particles closer to the fist fly faster. then it's gone. no continuous force, just one kick.

---

## project structure

```
gravity-god/
└── index.html    # everything — physics, rendering, hand tracking, UI
```

one file. no node_modules. no build. deploys in 30 seconds.

---

## tips

- **face a light source** — backlit hands are hard for MediaPipe to track. face a window or lamp for best detection.
- **the supernova moment** — crush everything into a ball with your fist for a few seconds, then snap your hand open. that's the one.
- **pinch-spam** — flood the screen with matter before doing anything else. more particles = more chaos.
- **two-palm tug-of-war** — get a fist-compressed ball then switch to two palms on opposite sides of it.

---

## author

**Aayush Sharma** — B.Tech CSE, Bennett University
NLP researcher · ML practitioner · apparently also a god of gravity

[![GitHub](https://img.shields.io/badge/GitHub-AayushSharma1003-181717?style=flat-square&logo=github)](https://github.com/AayushSharma1003)

---

also check out the other projects in this series:

- [**gesture sorcery**](https://aayushsharma1003.github.io/gesture-sorcery/) — wield ancient powers: fire, energy blasts, a summoned blade
- [**reality glitch**](https://aayushsharma1003.github.io/reality-glitch/) — tear your webcam feed open with GPU shaders

---

## license

MIT — do whatever you want with it.

---

