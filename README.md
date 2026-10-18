# Orbit: Space exploration quiz

A space exploration quiz for curious minds, built as a single self-contained
HTML file. No server, installation, dependencies, or network connection required.

## Play

Download or clone this repository and open `index.html` in your browser.

Answer ten multiple-choice questions about the solar system, space missions,
and the universe. Select an option with your mouse or use keys **1-4**. Use
**Tab** to navigate buttons and **Enter** or **Space** to activate them.

## Features

- Mission-control-style question and score readouts with an answer progress bar.
- Green correct-answer feedback and a red shake for incorrect answers, with
  explanations and the correct answer revealed.
- Results with accuracy, correct/incorrect totals, an emoji reaction,
  original-order replay, and shuffled replay.
- A narrow, responsive layout with an illustrated planet, hex grid, stars,
  and soft nebula glows.
- Automatic light/dark themes and reduced-motion support.
- Accessible buttons, focus transitions, live score and feedback announcements,
  and labeled progress.

## Development

All markup, styles, artwork, question data, and behavior live in `index.html`.
Edit the file and reload the browser to see changes.

There is no build step or configured test/lint runner. Browser checks and
implementation conventions are documented in
[the Copilot instructions](.github/copilot-instructions.md).

For a quick smoke test, select Mars on the first question and confirm the score
becomes one point; replay with Venus to check incorrect feedback. Complete the
quiz to check results and replay, then check both color schemes and a narrow
viewport.
