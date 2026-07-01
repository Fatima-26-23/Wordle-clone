# Wordle Clone

A custom Wordle clone built with React and Tailwind CSS, featuring a themed UI, dark mode, hard mode, colorblind support, and a live word-fetching + dictionary-validation system.

## Features

- **5-letter word guessing** — classic 6-guess Wordle gameplay
- **Live word source** — fetches a random 5-letter word from the [Random Word API](https://random-word-api.herokuapp.com/), then confirms it's a real dictionary word via the [Free Dictionary API](https://dictionaryapi.dev/), with a hardcoded fallback word list if either API is unavailable
- **Guess validation** — checks each submitted guess against the dictionary API before accepting it (fails open if the API is unreachable)
- **Hard Mode** — previously revealed correct/present letters must be reused in later guesses; can only be toggled before the first guess
- **Colorblind Mode** — swaps green/yellow tile colors for orange/blue
- **Dark Mode** — full light/dark theme toggle, with matching sun/moon illustration
- **On-screen + physical keyboard support** — keys are color-coded based on guess history
- **Settings modal** — toggle Dark Mode, Hard Mode, Colorblind Mode, or start a New Game
- **Help modal** — explains tile colors and how to play
- **Win/loss states** — confetti animation on win, reveals the answer on loss
- **Custom "Bubblegum"-style SVG title** using the Baloo 2 font
- **Responsive layout** — scales down for small screens

## Tech Stack

- **React** (hooks: `useState`, `useEffect`, `useCallback`)
- **Tailwind CSS** for styling
- **lucide-react** for icons (`Settings`, `X`, `Delete`, `Info`)
- **Free Dictionary API** and **Random Word API** for word sourcing/validation

## Project Structure

```
App.jsx
├── fetchRandomWord()     # gets today's word (API + dictionary check, with fallback list)
├── getStatuses()         # computes correct/present/absent for a guess
├── Wordle (default export)  # main game component + state/logic
├── Confetti               # win celebration animation
├── BubbleTitle             # stylized "WORDLE" SVG-style title
└── Toggle                  # reusable settings toggle switch
```

## How to Play

1. Guess the 5-letter word in 6 tries.
2. After each guess, tiles change color:
   - **Green** (or orange in Colorblind Mode) — correct letter, correct position
   - **Yellow** (or blue in Colorblind Mode) — correct letter, wrong position
   - **Gray** — letter not in the word
3. Use the on-screen keyboard or your physical keyboard to type guesses.
4. Toggle Hard Mode, Colorblind Mode, or Dark Mode from the Settings menu (⚙️).

## Setup

This component expects to run inside a React + Tailwind CSS (v4) project with `lucide-react` installed:

```bash
npm install lucide-react
```

Then drop `App.jsx` into your project as the root component.

## Run Locally

```bash
npm install
npm run dev
```

Then open the local URL shown in the terminal (usually `http://localhost:5173`) in your browser.

## Notes

- The two Sun/Moon illustrations are embedded as base64-encoded WebP images directly in the component.
- If both the word API and dictionary check fail, the game falls back to a small built-in word list (APPLE, BRAVE, CRANE, etc.).
- Word validation calls the dictionary API on every submitted guess, so an internet connection is required for full functionality (though the game won't block you if the API is down).
- ### For .css file:
- As we have included the styles in the App.jsx file we don't need a separate .css file. If you want you can add your own styles here and link it to the App.jsx file as import "./index.css";
