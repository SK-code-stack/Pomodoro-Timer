# ANSWERS.md



## 1. How to Run

No install needed. Just open `pomodoro-timer.html` in any modern browser — double-click works fine.

or visit this 
https://sk-code-stack.github.io/Pomodoro-Timer/


## 2. Stack & Design Choices

Why vanilla HTML/CSS/JS: Honestly, for a single-screen timer app, pulling in React or Vue would've been overkill. There's no complex state tree, no routing, no component reuse across pages. Vanilla JS kept the whole thing in one file with zero build setup — which also means anyone can open it instantly without touching a terminal.

Decision 1 — The SVG ring as the primary timer display
I made the countdown ring the visual centerpiece instead of just putting big numbers on screen. The ring fills and drains as time passes, so at a glance you can see how far along a session is without reading the digits at all. It takes up most of the card's vertical space on purpose — when you're heads-down working, you want to be able to look up and know "I'm about halfway through" without any mental effort. The numbers are still there in the middle for precision, but the ring does the heavy lifting.

Decision 2 — Full theme switch between focus and break (green vs blue)
When the mode changes, the entire UI recolors — the ring gradient, the glow on the card, the badge, the particles, the buttons, even the background haze. I didn't want the state change to be subtle. If you glance over and the screen is green you're focusing, blue means break. That way you don't have to read anything to know where you are in the cycle. This also made the automatic transition feel like an actual event rather than just a counter resetting.



## 3. Responsive & Accessibility

Responsive behavior:
On a 360px phone the layout stacks vertically — the ring shrinks from 260px to 220px, the focus/break inputs stack on top of each other instead of sitting side by side, and the button grid goes to single column. Font sizes use `clamp()` throughout so the timer digits scale smoothly rather than snapping between breakpoints. On a 1440px laptop it stays centered in a 500px max-width container — it doesn't stretch or go full-width because a timer that spans 1400px looks absurd.

Accessibility I handled:
All interactive buttons have explicit `font-weight` and clear background contrast against the dark card. The color scheme was chosen so the green (focus) and blue (break) pass contrast ratio requirements against the near-black background. The timer digits are large enough to read from a distance without straining.

Accessibility I skipped:
Proper ARIA live regions. Ideally the timer would have something like `aria-live="polite"` so screen readers announce the countdown and mode changes without the user having to navigate to the element. I skipped this because it would need careful tuning — announcing every single second would be unbearable, so you'd want to announce only on minute changes or mode switches, which requires a bit more state tracking. Given the time I had, I focused on the visual side and left this as a known gap.



## 4. AI Usage

I used Claude (Anthropic) throughout this project.

What I asked and what it gave me:

- Asked it to build the initial Pomodoro timer — got a working HTML/CSS/JS file with a basic dark UI, start/pause/resume/reset buttons, localStorage history, and a countdown.
- Asked it to redesign the visuals to be more eye-catching — it introduced the SVG ring, glassmorphism card, Orbitron font, floating particles, and the overall dark space aesthetic.
- Asked it to add auto-cycling, sounds, and a turns system — it wired up Web Audio API tones, removed the alert() calls and replaced them with a slide-in toast, added the infinite/fixed toggle, and built the turns countdown banner.
- Asked it to change the focus color to green and break color to blue — it updated the CSS variables, SVG gradient stops, glow colors, particle arrays, and flash overlay to match.

Something I specifically changed:

The AI initially played sounds by loading an external `.ogg` file from a Google URL: `new Audio('https://actions.google.com/sounds/v1/alarms/beep_short.ogg')`. That's a problem — if you're offline, or Google changes that URL, the sound just silently breaks. I had it replace this entirely with the Web Audio API, generating tones programmatically. The focus-complete sound became three ascending sine wave notes (C→E→G), the break-complete sound became three descending warmer tones, and there's a short fanfare when all turns finish. No external files, no network dependency, works offline, and the sounds are actually more satisfying than a generic beep.



## 5. Honest Gap

The session history is pretty bare. It shows "✓ 25:00 focus — 3:42pm" as a line item, which works, but there's no daily summary, no total focus time, no sense of progress across the week. If I had another day I'd add a small stats bar at the top of the history section — something like "Today: 2h 5m focused across 5 sessions" — and maybe a tiny spark-line or dot-grid showing which hours of the day you were active. That would make the history feel like it means something rather than just a log you scroll past.