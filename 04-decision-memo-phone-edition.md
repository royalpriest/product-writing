# Decision Memo: Give Phones Their Own Edition of the Portfolio

**Product:** Royalpriest portfolio ([royalpriest.dev](https://royalpriest.dev), phone edition at [royalpriest.dev/film](https://royalpriest.dev/film))
**Type:** Decision memo
**Status:** Shipped, November 2026

> Adapted from the portfolio's design notes and change history for public reading. It covers the problem, the options and how each choice was judged, not the code.

## Decision

Phones get a separate design, the **film edition**, instead of a shrunk copy of the desktop. Desktop keeps its retro desktop of windows. Both editions live on one page with the same content, and each device loads only what its own edition needs.

## Problem

The desktop portfolio is an explorable retro computer: draggable windows, a pixel companion, a tools drawer, a Standby screensaver. That idea depends on a big screen and a mouse. On a phone, windows become stacked boxes, hover hints never appear, and the charm turns into clutter. A recruiter opening the link on their phone, which is often where a link is first opened, saw the weakest version of the work.

## Options considered

| Option | Why not (or why) |
| --- | --- |
| Responsive desktop: stack the windows | Cheapest, but keeps a metaphor that doesn't fit a phone. Rejected. |
| A plain mobile résumé page | Clear, but throws away the personality that makes the portfolio memorable. Rejected. |
| A separate site for phones | Two codebases and two sets of content that drift apart. Rejected. |
| **A second edition on the same page, with its own concept** | One set of content and one link, and a design built for a thumb and a small screen. **Chosen.** |

## The concept: a love letter to film

The phone edition reads like a film. Sections are **scenes** laid side by side like frames on a film strip: swipe sideways to change scene, scroll down within one.

1. **Opening:** a sky that follows the visitor's local time, "Written & directed by", the name and a short intro.
2. **Features:** one project at a time, its clip playing on a projector screen, with Director's notes (the case study) below.
3. **Credits:** experience, education and learning.
4. **Behind the scenes:** about, Equipment (tools) and How I work.
5. **Screening room:** favourite films, books, games and a soundtrack.
6. **Post-credits:** contact and *Fin.*

The theme is the voice, not the facts. Job titles, dates and "Open to opportunities" stay literal, so the playfulness never makes the career harder to read.

## How the choices were made: prototypes behind a switch

Each uncertain choice shipped as two or three live prototypes, selectable with a link parameter, and was picked on a real phone before it became the default. Losing options were removed rather than kept as settings.

- **Navigation:** sideways scene swiping versus one long page. Swiping won; the long page stays as a fallback.
- **Project clips:** flat screen, CRT or framed, then a projector screen with or without a countdown. The projector won and the countdown was cut.
- **Neon:** three styles for the tech stack reel. Soft tubes won, and were tried on desktop too, then held back there because they didn't suit it.
- **Player dock:** gloss versus matte film grain. Smoked matte glass with a dim neon edge won.
- **Intermission:** a phone version of the desktop's Standby screen, with a lock-screen-style glass clock and my own wallpapers seen through an arched window.

## Making it feel fast, not just look good

A beautiful phone edition that flashes and stalls on reload undoes the first impression. Three problems were fixed after testing on real devices:

- **No flash of the wrong edition.** The server marks the page as the phone edition before the first paint, so phones no longer flash the desktop's unstyled text on every reload.
- **No re-checking every file.** Files are named by their contents and kept by the browser. A phone reload went from **52 re-check requests to none**.
- **Quiet first seconds.** Decorative motion waits until the page settles, which **halved the phone's main-thread work in the first four seconds** (about 43% to 22% on a throttled CPU). The phone's fonts are self-hosted, so nothing waits on a third party.

Real-device testing also caught a bug no desktop browser showed: on iPhone, the rolling rows of covers seemed to run out mid-loop. The rows were rebuilt in an iPhone-safe pattern and sized so they never depend on how a browser measures images.

## Sharing

One link can only show one preview, so the phone edition got its own link, `/film`, with its own preview card. A **Pass it on** button opens the phone's share sheet. Opening `/film` on a computer shows the phone edition inside a phone frame, so it can be shared and viewed anywhere.

## How success is judged

- The phone edition is reviewed on real phones, iPhone included, not only in a desktop browser's phone view.
- Reloads show no flash of the desktop and make no unnecessary requests.
- Content stays identical across editions, with nothing that exists on only one.
- Motion respects reduced motion and a Motion off toggle everywhere.

## What stays out

The desktop-only toys (the board, display settings, pixel playground and guided tour) are not part of the phone edition. They depend on a pointer and a big screen, and forcing them in would repeat the original problem.
