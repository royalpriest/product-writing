# Proposal: Show Visitors Their Own Weather Without Asking for Their Location

**Product:** Royalpriest portfolio ([royalpriest.dev](https://royalpriest.dev))
**Type:** Feature proposal
**Status:** Shipped, November 2026

> Adapted from the portfolio's change history for public reading. It covers the problem, the product rules and the privacy choices, not the code.

## Problem

The portfolio's scenes already change with the visitor's local time: morning haze, afternoon, last light, night. But the sky was always a guess. It could show a clear evening while the visitor sat in a rainstorm. A small detail that matches the visitor's real day makes the site feel present; one that's wrong makes it feel canned.

The obvious fix, asking for the visitor's location, is the wrong trade. A permission prompt on a portfolio feels intrusive, most people decline it, and a recruiter shouldn't have to make a privacy decision to read a résumé.

## Proposal

Show the visitor's live local weather on the Opening card, in Intermission and in Standby, **with no prompt by default**.

1. **Approximate by default.** The hosting platform already knows each visitor's rough city from their connection. The site uses that, rounded to about 10 km, to look up current weather.
2. **Precise only when asked.** Tapping the weather offers **Use my location**. Only then does the browser ask, the position is rounded to about 1 km, and the choice is remembered.
3. **Quiet when unsure.** With no location or no weather, the scene falls back to the time-of-day sky. Nothing breaks and nothing nags.

## Privacy rules

- The visitor's browser never talks to a weather service. Only the site's server does, and it sends only rounded coordinates, so the visitor's IP address never leaves the host.
- Coordinates are rounded before they are used: about 10 km by default, about 1 km if the visitor opts in.
- The weather service needs no account or key, and readings are cached per area for 15 minutes, so the site makes few requests and keeps no per-visitor history.
- Town names for opted-in visitors come from OpenStreetMap, also looked up by the server.

## Design rules

- One quiet line: short date, a weather icon, temperature and town. No forecast, no widget.
- Weather sets the sky's mood; it never covers content.
- The feature is invisible when it can't help.

## How success is measured

- No location prompt appears unless the visitor taps **Use my location**.
- The shown town and conditions match reality in spot checks from several cities.
- Pages load just as fast with weather on; a slow or failed lookup falls back to the time-of-day sky.

## Scope

Weather only changes the atmosphere of three scenes. It doesn't change content, order or anything a visitor needs to read the portfolio.
