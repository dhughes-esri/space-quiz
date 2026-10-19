# Copilot Instructions

## Build, test, and lint

- The app is a standalone `index.html`; open it directly in a browser to run it. No server or dependency installation is needed.
- There is no configured build, test, or lint command.

## Architecture

- `index.html` contains the entire application: semantic page markup, CSS in `<style>`, and quiz logic in an inline `<script>`. Keep the page self-contained; there is no package manifest or separate runtime.
- The `questions` array is the source for question content, answer choices, correct-answer indexes, and explanations. `questions.length` drives the score denominator and progress. The UI text also describes the quiz as ten questions, so keep it in sync if the question count changes.
- Quiz state (`currentQuestion`, `score`, `answered`) is managed in the script. `renderQuestion()` builds the answer buttons, `chooseAnswer()` scores and locks the current choices, and the next/restart handlers advance, show results, or reset the quiz.

## Project conventions

- Keep visual styles in the existing `<style>` block and use the color tokens in `:root` for shared palette values. The mobile layout uses a 520px breakpoint.
- Keep questions data-driven in the existing object shape; answer buttons are created in `renderQuestion()`, and their visible text is assigned with `textContent`.
- Preserve the accessibility patterns: native buttons, a labeled progress bar, live regions for score and feedback, visible `:focus-visible` styling, and focus movement to the new question or results heading.
- Respect the existing `prefers-reduced-motion` rule when adding animations or transitions.
