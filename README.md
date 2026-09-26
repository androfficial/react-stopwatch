# Stopwatch

Stopwatch built on RxJS streams: start and stop it, pause it with a double click on Wait, or reset it. Built in December 2021 as a take-home assignment.

**Live demo:** [react-stopwatch-androfficial.vercel.app](https://react-stopwatch-androfficial.vercel.app)

## Features

- Shows the elapsed time as `HH:MM:SS`, and the ring around it rotates while the stopwatch runs.
- Start counts on from the current time, so after Wait it resumes where it paused.
- While the stopwatch runs, the same button reads Stop: it halts the count and sets the time back to `00:00:00`.
- Wait pauses the count and keeps the time, but only on a double click (two clicks within 300 ms). A single click does nothing.
- Reset sets the time to `00:00:00` and starts counting again straight away, whether the stopwatch was running or not.

## Tech stack

- **Framework:** React 17
- **State:** React state driven by RxJS 7 streams
- **Styling:** SCSS (Dart Sass 1), classnames, a CSS keyframes animation for the ring, local Gilroy fonts
- **Tooling:** Create React App 5 with react-app-rewired, Stylelint 14 in the development build, ESLint 8 and Prettier 2 configs
- **Hosting:** Vercel

## Getting started

Requires Node.js 16 or 18 and Yarn 1.

```bash
git clone https://github.com/androfficial/react-stopwatch.git
cd react-stopwatch
yarn install
yarn start
```

## Scripts

| Command | Description |
| --- | --- |
| `yarn start` | Starts the development server |
| `yarn build` | Builds the production bundle into `build/` |

## Project structure

```text
src/
  components/   App: the stopwatch screen, its state and the RxJS subscriptions
  services/     timeFormatting: seconds to HH:MM:SS
  styles/       SCSS: local fonts, mixins, reset, buttons
```

## Notes

- The tick is an RxJS `Observable` wrapping a one-second `setInterval`, subscribed again whenever the running state changes. The Wait button is a `fromEvent` click stream buffered with `debounceTime(300)` and filtered to groups of two or more clicks.
- Stylelint runs inside the development build through `config-overrides.js` (react-app-rewired).
