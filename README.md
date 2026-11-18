# Product Writing Samples

Hi, I'm Royalpriest Babalola. These are writing samples from products I've built and run: decision memos and feature proposals from **[SaintFlick](https://saintflick.com)**, an AI-assisted movie discovery app, and from **[my portfolio](https://royalpriest.dev)**, an explorable retro desktop with a separate film-themed phone edition.

I write a short doc before each significant change: the problem, the options, the decision, and how we'll know it worked. These are adapted from those docs for public reading. They focus on problems, options and decisions; how the system works under the hood has been left out.

### SaintFlick

| Doc | Type | What it decided |
| --- | --- | --- |
| [Stay PWA-first instead of wrapping as a native app](01-decision-memo-pwa-first.md) | Decision memo | Keep shipping one installable web app. Weighed five options on cost, store policy and user value, and defined exactly when a native app becomes worth it. |
| [Friend Mode: movies two people will both accept](02-proposal-friend-mode.md) | Feature proposal | Never override anyone's "no," let preferences shape results without blocking them, and favour picks that work for both people over lopsided ones. |
| [Make "Why This Fits" explain the real reason](03-proposal-explain-match.md) | Problem statement and fix | Base explanations on the real reason a movie was picked, so they can't contradict the recommendation. |

### Portfolio

| Doc | Type | What it decided |
| --- | --- | --- |
| [Give phones their own edition of the portfolio](04-decision-memo-phone-edition.md) | Decision memo | Build a film-themed phone edition instead of shrinking the desktop, choose each detail from live prototypes on a real phone, and make reloads fast (52 re-check requests to none). |
| [Show visitors their own weather without asking for their location](05-proposal-live-weather.md) | Feature proposal | Use rounded, approximate location by default and precise location only on request, so the scenes match the visitor's real sky without a permission prompt. |

## How I write these

- **Lead with the decision.** The first lines say what was decided and why.
- **Compare real options.** I list the alternatives I rejected and why.
- **Define success up front.** Each proposal says how it will be measured, including a human review.
- **Keep the negative results.** Experiments that didn't work are recorded, not deleted.

## Other products

- **[Storikeep](https://storikeep.com):** a personal library for movies, TV, books and games, in closed beta.
- **[NorthStar Baseball](https://northstar-baseball.vercel.app):** a baseball analytics app built on validated metrics.

[Portfolio](https://royalpriest.dev) · [LinkedIn](https://linkedin.com/in/royalpriest-babalola)
