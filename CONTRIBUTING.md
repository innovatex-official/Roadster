# Contributing

Thanks for taking a look at **Roadster: Launch Night**.

## How this repository is structured

The game is shipped as a **single prebuilt file**, `index.html`. All 300+ source
modules are embedded inside it as text and wired together at load time by a small
bootstrap script. This keeps deployment trivial (one static file, zero build
step) at the cost of the file being large and not directly hand-editable.

Because of that, please note:

- **Do not hand-edit `index.html`.** It is a build artifact. Edits should be made
  in the original module sources and rebuilt.
- If you are only reporting a bug or suggesting a feature, open an issue instead
  of a pull request against the built file.

## Reporting issues

A good bug report includes:

1. What you did, step by step.
2. What you expected to happen.
3. What actually happened.
4. Browser and version, OS, and whether WebGL 2 is available.
   (Visit `chrome://gpu` / `about:support` if unsure.)
5. A screenshot or clip if the bug is visual.

## Running and testing

Serve the folder and open it in a browser:

```sh
python3 -m http.server 8080
# http://localhost:8080
```

WebGL 2, ES modules and import maps are required. Test in both a desktop and a
narrow (mobile) viewport before submitting visual changes — the HUD reflows
heavily below 860px.

## Style

- Match the conventions of the surrounding code.
- Keep changes focused; one concern per pull request.
- Respect `prefers-reduced-motion` — the HUD already does.

## Licence

By contributing you agree that your contributions are licensed under the
project's [MIT Licence](./LICENSE).
