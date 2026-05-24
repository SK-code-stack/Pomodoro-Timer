# Pomodoro-Timer

A single-screen Pomodoro timer built with vanilla HTML, CSS, and JavaScript. No build step, no dependencies, no npm install — just open the file and it works.

---

## How to Run

### Option 1 — Just open it (simplest)

```bash
open pomodoro-timer.html
```

Or double-click the file in your file explorer. It opens directly in any modern browser (Chrome, Firefox, Safari, Edge).

### Option 2 — Local dev server (if you want a proper localhost URL)

If you have Python installed (comes pre-installed on Mac and most Linux):

```bash
python3 -m http.server 8080
```

Then visit: [http://localhost:8080/pomodoro-timer.html](http://localhost:8080/pomodoro-timer.html)

Or with Node.js:

```bash
npx serve .
```

Then open the URL it prints.

### Requirements

- A modern browser (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)
- That's it. No Node, no npm, no build tools required.

---

## Features

- Configurable focus and break durations
- Auto-cycles focus → break → focus without any clicks
- Audible cues when each phase ends (built with Web Audio API — no audio files needed)
- Fixed turns mode: set how many cycles to run, or leave it on infinite
- Live turns counter in the header that counts down each break
- Full daily session history that persists through page reloads and resets on a new calendar day
- Fully responsive — works on 360px phones up to wide desktop screens

---

## Project Structure

```
pomodoro-timer.html   ← entire app (HTML + CSS + JS in one file)
README.md
ANSWERS.md
```