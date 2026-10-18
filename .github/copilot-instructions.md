# Orbit space quiz

## Run and browser checks

Open `index.html` directly in a browser or the integrated browser using its
absolute `file:///` URL. The application must remain usable without a server,
dependencies, or network access.

There are no build, test, or lint commands or configured test runner. Validate
changes in the browser. To check one scenario, reload the page and exercise only
the relevant flow:

- Correct answer: choose Mars on question 1 (shortcut `2`); expect `1 point`,
  green feedback, an explanation, and progress `1` of `10`.
- Incorrect answer: choose Venus on question 1 (shortcut `1`); expect `0 points`,
  a red shake, and Mars revealed as the correct answer.
- Keyboard flow: check native Tab/Shift+Tab and Enter/Space separately from the
  `1`-`4` shortcuts. Selecting an answer focuses Next; advancing focuses the
  question heading; results focus their heading; replay focuses question 1.
- Results: complete all ten questions and verify score, accuracy, incorrect
  count, completed progress, and emoji. Reaction thresholds are `0`-`3`,
  `4`-`6`, `7`-`9`, and `10` correct. Replay resets all quiz state.
- Appearance: check light and dark preferences, reduced motion, and widths of
  320, 375, and 540 CSS pixels for overflow and readable telemetry.

The integrated browser supports local-file previews. Some automation browsers
block `file:` URLs; report that limitation rather than claiming native keyboard
coverage from synthetic DOM events.

## Architecture and state

The entire application is `index.html`: inline CSS, semantic HTML, inline SVG
artwork, and a classic inline JavaScript script. Keep implementation and assets
self-contained; there is no framework, backend, routing, or persistent storage.

The `questions` array holds ten records with `category`, `question`, four
`options`, a zero-based `answer` index, and explanatory `fact`. `current` is a
zero-based question index; `score`, `answered`, and `finished` control the flow.
`renderQuestion()` creates options and clears feedback, `selectAnswer()` locks
the answer and updates feedback/score/progress, and `showResults()` switches
screens. Both clicks and number shortcuts use `selectAnswer()`.

Progress counts answered questions, not the displayed question number. A wrong
answer still advances progress. The ten-question assumption also appears in
HTML labels, progress limits, percentage calculations, and result denominators;
changing quiz length requires updating all of these together.

## UI conventions

- Maintain the centered 540px maximum column, sans-serif 15px body, mission
  telemetry readouts, and space-inspired visual language.
- Theme colors are CSS custom properties in `:root`, with light overrides under
  `prefers-color-scheme: light`; dark is the base theme. Use these tokens for
  new UI surfaces rather than introducing one-theme colors.
- Background stars/glows and SVG-masked hexes live in fixed body pseudo-elements
  with `pointer-events: none`; `.page` sits above them at `z-index: 1`. Keep both
  standard and WebKit mask declarations in sync.
- `.correct`, `.wrong`, and `.dim` express answer states. Feedback combines
  color with symbols and explanatory text. Reduced-motion preferences disable
  animation and transitions without hiding feedback.
- Preserve the native option buttons, disabled Next gating, heading focus
  targets (`tabindex="-1"`), valid `aria-labelledby` references, score live
  region, feedback status region, and progressbar ARIA values.
- Use the existing `$` selector helper and DOM creation/textContent pattern for
  question content. Toggle screens with `hidden`; its CSS rule is intentional.
  Result emoji are encoded with JavaScript Unicode escapes.
