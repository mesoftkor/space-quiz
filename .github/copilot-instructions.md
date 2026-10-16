# Copilot instructions

## Build, test, and lint

- This is a standalone static page in `index.html`; open that file in a browser to run it.
- The repository has no package manifest, build scripts, lint scripts, or automated test runner. There is no configured single-test command.

## Architecture

- `index.html` contains the entire app: semantic quiz/results markup, embedded responsive and theme-aware CSS, the question bank, and the JavaScript that drives the quiz. There is no separate client/server layer or build step.
- The question bank is an array of objects near the start of the script. Each entry has a category, question, four options, a zero-based `correct` option index, and an explanation.
- The script keeps quiz progress in `current`, `score`, `selections`, and `finished`. `renderQuestion` and `showResults` derive the screen from that state; `chooseAnswer`, `nextQuestion`, and `restart` handle state transitions.
- DOM references are collected in the `ui` object. Dynamic content is built with DOM methods and assigned with `textContent`, rather than interpolated as HTML.

## Codebase conventions

- Keep changes within the single-file structure unless the task calls for a deliberate extraction; there is no module or asset pipeline.
- Keep the question data as the source of truth for question count and answer correctness. The correct answer is stored as a zero-based option index.
- Preserve the existing accessibility behavior when changing interactions: answer and navigation buttons, progress and live-status semantics, number-key shortcuts, and focus movement are part of the quiz flow.
- Visual behavior is defined by CSS custom properties, including `prefers-color-scheme` theme values. Responsive layouts use narrow-width media queries, and motion is gated by `prefers-reduced-motion`.
