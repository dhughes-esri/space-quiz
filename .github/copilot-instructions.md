# Copilot Instructions

## Build, test, and lint

- The app is a standalone `index.html`; open it directly in a browser to run it. No server or dependency installation is needed.
- There is no configured build, test, or lint command.

## Architecture

- `index.html` contains the entire application: semantic page markup, CSS in `<style>`, and quiz logic in an inline `<script>`. Keep the page self-contained; there is no package manifest or separate runtime.
- The `questions` array is the source for question content, answer choices, correct-answer indexes, and explanations. `questions.length` drives the score denominator and progress. The UI text also describes the quiz as ten questions, so keep it in sync if the question count changes.
- Quiz state (`questionOrder`, `currentQuestion`, `score`, `answered`, and `selectedAnswers`) is managed in the script. `questionOrder` shuffles the questions for each game; `selectedAnswers` is indexed in that shuffled order so `renderReview()` can display the matching choices. `renderQuestion()` builds the answer buttons, `chooseAnswer()` stores the selection and updates scoring, and the results/review and restart handlers switch screens or reset the quiz state.
- The theme picker applies CSS themes through `data-theme` on the root element. Theme choice and personal-best score are persisted separately in `localStorage`; preserve the existing graceful handling and warnings when browser storage is unavailable.

## Project conventions

- Keep visual styles in the existing `<style>` block and use the color tokens in `:root` for shared palette values. The mobile layout uses a 520px breakpoint.
- Keep theme variants in the existing `:root[data-theme]` rules and keep the theme picker's values aligned with the `themes` set in the script.
- Keep questions data-driven in the existing object shape; answer buttons are created in `renderQuestion()`, and their visible text is assigned with `textContent`.
- Preserve the accessibility patterns: native buttons, a labeled progress bar, live regions for score and feedback, visible `:focus-visible` styling, and focus movement to the new question or results heading.
- Respect the existing `prefers-reduced-motion` rule when adding animations or transitions.
