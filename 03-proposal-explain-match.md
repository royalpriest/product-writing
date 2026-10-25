# Proposal: Make "Why This Fits" Explain the Real Reason

**Product:** SaintFlick, an AI-assisted movie discovery app ([saintflick.com](https://saintflick.com))
**Type:** Problem statement and fix
**Status:** Shipped

> Adapted from SaintFlick's internal design docs for public reading. How the system works under the hood has been left out; this covers the problem, the product rules and how success was judged.

## Problem

Every SaintFlick recommendation has a "Why This Fits" button that explains why a movie suits the viewer's request.

The explanation was written separately from the recommendation itself, using little more than the movie's description and the viewer's mood. It didn't know **why the movie was actually recommended**.

The result: explanations that sounded plausible but could contradict the real reason for the pick. That quietly erodes trust. If the explanation doesn't match the recommendation, users stop believing either one.

## Proposal

Make "Why This Fits" a faithful explanation of the actual recommendation, not a second, independent opinion.

1. **One source of truth.** The explanation is based on the reason the movie was picked. It must never contradict it.
2. **Fair in two-person mode.** When two people choose together, the explanation describes what works for both, not just one of them.
3. **Nuance without the machinery.** For a request like "romantic and warm, not cheesy," the explanation can speak to restraint or natural warmth, but it never exposes scores or system internals.

## Output rules

Each explanation must be:

- exactly one concise sentence, 26 words at most
- free of generic praise ("a must-watch!")
- free of invented plot or theme claims
- free of technical jargon about how the app works

The "Why This Fits" design stays visually unchanged. Only what it says changes.

## How success is measured

A regression test set checks every explanation for:

- faithfulness: does it reflect the real reason for the pick?
- format: one sentence, within the 26-word limit
- jargon: does any technical language slip into what users see?
- reliability and response time
- a human review of whether it rings true

## Scope

This change affects only the explanation. Which movies get recommended is deliberately untouched, so the fix can't change what people are offered.
