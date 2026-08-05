# Clock Suite

A small, dependency-free collection of time tools: a digital clock, a flip clock, a timer/stopwatch, and a world clock/time zone converter. Each tool is its own static HTML page, linked together by a shared top navigation dropdown, so the whole suite can be hosted as-is with no build step or server-side code.

## Pages

### `index.html` — Digital Clock
- Live seven-segment-style clock built from SVG polygons (no images/fonts for the digits).
- 12-hour / 24-hour format toggle.
- Optional seconds display and an optional "day and year" date line.
- Nine color/style templates (Digital, Digital-Blue, Digital-Red, Digital-Amber, Digital-Orange, Pure Dark, Dark, Light, Classic) selectable from a settings sidebar.

### `flipclock.html` — Flip Clock
- Same clock engine and settings sidebar as the digital clock, styled as flipping mechanical-style units instead of seven-segment digits.
- Same format/seconds/date toggles and template picker.

### `timer.html` — Online Timer (Countdown & Stopwatch)
- Two modes: **Countdown** and **Stopwatch**, switchable from the top of the page.
- Countdown: set hours/minutes/seconds manually or via quick-set presets, start/pause/reset, and an audible beep when it reaches zero.
- Stopwatch: start/pause/reset plus lap recording with a lap list.
- Uses the same seven-segment SVG digit renderer as the clock pages.

### `worldclock.html` — Time Zone Converter and World Clock
- A grid of live clocks for a configurable list of cities, each showing local time, date, and UTC offset.
- Add/remove cities from a searchable city selector.
- A separate time zone converter: pick a "from" zone and date/time and a "to" zone to see the converted time, with a swap button to flip the two zones.
- 12/24-hour format toggle and a day/night indicator switch.
- Uses the browser's `Intl.DateTimeFormat` API for all time zone math (no external time zone library).

## Shared UI elements

All four pages share:
- A **top bar** with a brand mark, a dropdown to jump between the four tools, and icon buttons for fullscreen, "keep screen awake" (via the Screen Wake Lock API), and a settings toggle.
- A **collapsible settings sidebar** on the right for that page's options.
- The same dark, high-contrast visual style (black background, white/blue accents), defined per-page in an inline `<style>` block.

## Tech stack

- Plain HTML, CSS, and vanilla JavaScript — no frameworks, build tools, or external JS dependencies.
- Digits are hand-drawn as SVG polygons and toggled on/off per segment, rather than using a webfont or images.
- Browser APIs used: `Intl.DateTimeFormat` (time zones), Fullscreen API, Screen Wake Lock API, and an audible beep for the timer alarm.
- Each page embeds its own favicon as a base64 data URI, so there are no separate image assets to serve.

## File structure

```
.
├── index.html         # Digital Clock
├── flipclock.html     # Flip Clock
├── timer.html          # Countdown Timer & Stopwatch
└── worldclock.html     # World Clock & Time Zone Converter
```

## Running it

These are static files — just open `index.html` (or any of the other pages) directly in a browser, or serve the folder with any static file server. No installation or build step is required.

## Notes

- Settings (theme, format, toggles) are held in in-memory JavaScript state per page load; they are not currently persisted between visits or shared across the four pages.
- The Screen Wake Lock and Fullscreen buttons degrade gracefully (or silently fail) in browsers that don't support those APIs.
