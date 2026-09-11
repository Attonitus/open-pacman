# Agent Instructions

## Project Shape

- This is a dependency-free, browser-only Vanilla JS/HTML/CSS game; there is no package manifest, build step, test runner, or CI configuration.
- The runnable entrypoint is `src/index.html`; verify changes by opening it in a browser. No automated verification command is defined.
- The HTML loads classic scripts in this required order: `maze.js`, `game.js`, `render.js`, then `main.js`. They communicate through globals, so preserve that order unless deliberately migrating the whole wiring.
- `src/js/maze.js` owns the pristine 28x31 maze and spawn constants; `src/js/game.js` owns mutable game state and rules; `src/js/render.js` draws the canvas; `src/js/main.js` owns input, the animation loop, and overlay screens.
- `game.js` copies `MAZE` into each new game and mutates the copy as dots are eaten; do not mutate the source `MAZE` when adding gameplay behavior.
- The canvas is fixed at 28x31 tiles, 20px each (`560x620`); changes to tile geometry must stay consistent across the HTML canvas and renderer.

## Workflow

- The project follows spec-driven development. For substantial features, use `.agents/skills/spec/SKILL.md`; implement only approved specs according to `.agents/skills/spec-impl/SKILL.md`.
- With no build or test tooling, manually exercise the browser flow after gameplay changes: start/restart, arrow-key movement, dot collection/win, ghost collisions/lives, and loss/reset.
