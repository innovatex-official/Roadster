# Roadster: Launch Night

A self-contained, single-file WebGL browser game. Everything — the renderer, the
vehicle geometry, the physics, the audio engine and the UI — is embedded inside
one `index.html`. There is no build step, no server and no external asset
requests: open the file in a modern browser and the game runs.

> **Live demo:** deploy the repo to any static host (Vercel, GitHub Pages,
> Netlify, …) or just double-click `index.html`.

---

## Highlights

- **Six drivable vehicles**, each modelled procedurally from code — a Roadster,
  Model 3, Model Y, Cybertruck, Cybercab and Semi.
- **Custom vehicle physics** — tyre model, suspension, contacts, hulls and
  thruster forces, all simulated per-frame.
- **Launch / stunt gameplay** — J-ramp runs, kicker lanes, vertical hang,
  handbrake drifts, combos, scoring and an auto-land assist.
- **A bot-driven night session** — a lobby and room flow populated by AI
  opponents with live nameplates, a leaderboard and a commentary feed.
- **Synthesised audio** — engine, drivetrain, tyre scrape, crowd, reverb and a
  generative music score, all produced with the Web Audio API.
- **A full in-car UI** — touch-style screens for Charging, Climate, Dynamics,
  Lights, Listen, Navigate and Track Mode setup.
- **Cinematic rendering** — PMREM environment lighting, bloom, depth of field,
  SSAO, SMAA and a speed-line streak pass.

## Controls

Keyboard (default), gamepad and touch are all supported.

| Action | Key |
| --- | --- |
| Throttle / accelerate | `W` |
| Brake / reverse | `S` |
| Steer | `A` / `D` |
| Handbrake drift | `Shift` + `W` |
| Boost / thrusters | `Space` |
| Front trick | `ArrowUp` |
| Back trick | `ArrowDown` |
| Change camera | `C` |
| Toggle headlights | `L` |
| Open the in-car display | `Enter` |
| Guide / next objective | `G` |
| Pause / options / exit | `Escape` |

Additional bindings (`Q`, `E`, `H`, `R`, `V`, `X`, `Y`) toggle camera angles,
honk, reset, replay and other session options — the on-screen hints list them
as they become available.

## Running locally

Because everything is inlined, the simplest option is to open the file directly:

```sh
open index.html          # macOS
xdg-open index.html      # Linux
start index.html         # Windows
```

Some browser features (module workers, clipboard) behave better over HTTP, so
you can also serve the folder:

```sh
python3 -m http.server 8080
# then visit http://localhost:8080
```

## Deploying

The repo is a static site with a single entry point. On Vercel:

```sh
vercel login
vercel
```

Choose **Other** as the framework, the project root as the code directory and
`./` as the output directory — no build command is required. A `vercel.json` is
included with sensible defaults.

## Browser support

The game requires **WebGL 2**, **ES modules** and **import maps**:

- Chrome / Edge 89+
- Firefox 108+
- Safari 16.4+

If any of these are missing, the page shows a friendly message instead of
failing silently.

## Project layout

The repository deliberately ships one built artifact. Inside `index.html` the
logic lives in 300+ modules, embedded as text and wired up at load time. The
main areas are:

| Namespace | Responsibility |
| --- | --- |
| `js/main.js` | Entry point and boot sequence |
| `js/car`, `js/vehicles` | Procedural vehicle bodies, materials and trim |
| `js/phys` | Tyres, suspension, hulls, contacts, ramps, thrusters |
| `js/game` | Launch session, tricks, combos, replays, nameplates |
| `js/env` | Night arena, floodlights, jumps, sky, crowd, props |
| `js/fx`, `js/post` | Particles, skids, bloom, DoF, SSAO, SMAA, streaks |
| `js/audio`, `js/music` | Engine/drivetrain synthesis and the generative score |
| `js/rui` | In-car UI shell, screens, HUD and components |
| `vendor/three-r169` | Vendored [Three.js](https://threejs.org) r169 |

## Third-party code

- **Three.js r169** — MIT licence, © 2010–2024 Three.js Authors, vendored under
  `vendor/three-r169`.
- Fonts referenced by the UI (`Michroma`, `Saira`) fall back to system stacks if
  they are unavailable.

## Licence

See [`LICENSE`](./LICENSE). The bundled Three.js remains under its own MIT
licence.
