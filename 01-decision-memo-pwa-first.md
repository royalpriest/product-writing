# Decision Memo: Stay PWA-First Instead of Wrapping SaintFlick as a Native App

**Product:** SaintFlick, an AI-assisted movie discovery app ([saintflick.com](https://saintflick.com))
**Decision:** Keep SaintFlick as an installable progressive web app (PWA). Do not add a native app-store wrapper yet.
**Status:** Decided. Revisit when the native capability gate below is met.

> Adapted from SaintFlick's internal design docs for public reading. How the system works under the hood has been left out; this covers the options, the decision and when to revisit it.

## Decision

**Keep SaintFlick PWA-first. Do not add Capacitor (a native wrapper) to the production codebase yet.**

The current PWA already delivers the highest-value "app" behavior from one codebase:

- installable on desktop and mobile
- standalone display mode with a branded icon
- an offline-safe fallback screen
- safe-area handling on notched phones
- home-screen and Start-menu presence
- optional account continuity across devices
- native browser sharing where supported

A store wrapper is only worth adding when SaintFlick has native-only functionality that materially improves the product.

## Why a simple native wrapper is the wrong next step

SaintFlick is not a static website; much of what makes it useful runs on the server. A wrapper like Capacitor expects a bundle of static files, so making SaintFlick fit that model would mean reworking or removing core features.

The shortcut, pointing the wrapper at the live website, is something Capacitor's own documentation says is not intended for production.

## Store-policy reality

**iOS.** Apple's App Review Guideline 4.2 requires an app to offer functionality, content and UI beyond a repackaged website. Submitting the current PWA in a thin web-view wrapper adds review risk without adding user value.

**Android.** Google Play allows web-powered apps but still requires adequate functionality and a meaningful mobile experience. The existing PWA can be packaged for the store without restructuring the app first.

## Options evaluated

| Option | Engineering cost | Keeps one codebase | Native APIs | Store distribution | Fit now |
| --- | --- | --- | --- | --- | --- |
| PWA only | Low | Excellent | Limited | No app-store listing | **Best current fit** |
| Packaged PWA (Android / Microsoft Store) | Low–medium | Excellent | Limited | Android, Microsoft | **Good future Android path** |
| Capacitor wrapper | Medium–high | Good, after architecture work | Excellent | iOS, Android | **Not yet** |
| React Native / Expo rewrite | Very high | Poor | Excellent | iOS, Android | No |
| Fully native (Swift + Kotlin) | Extreme | None | Excellent | iOS, Android | No |

## What would justify a native app later

A native runtime becomes worthwhile when SaintFlick needs a **cluster** of native capabilities, not just a store badge. Candidates:

1. **Push notifications:** streaming-availability changes for watchlist titles, opt-in reminders, invitations to a shared session.
2. **Deep links:** shared movie links that open straight into the installed app; sign-in continuing inside the app.
3. **Native share integration:** receiving movie links shared from other apps.
4. **Haptics and system UI:** restrained feedback on save and swipe actions.
5. **Background tasks:** only if there is a legitimate background sync need.
6. **Widgets and shortcuts:** a quick "Find a film" action or a watchlist shortcut.

One cosmetic native feature is not enough reason to take on native projects, code signing, store review, release trains and platform-specific maintenance.

## Recommended roadmap

**Now:** keep the PWA as the production experience. Treat app-store presence as a distribution problem, not a reason to rewrite the product.

**Optional next step: Android distribution test.** If store visibility becomes useful, package the existing PWA for Android first, test it on a real device, and don't publish until it passes product and policy review.

This is lower-risk than introducing a native wrapper now.

**Native capability gate.** Start a native app only when **two or three native-only capabilities** have concrete product value and a plan behind them. At that point, build it as a real app on top of a shared backend rather than loading the website inside a wrapper, and check App Store Guideline 4.2 readiness before submitting.

## Acceptance criteria for this decision

- [x] Current PWA capabilities reviewed
- [x] Native-packaging constraints reviewed
- [x] Native wrapper fit assessed
- [x] App Store minimum-functionality risk identified
- [x] Android store-packaging path identified
- [x] Threshold for native-only features defined
- [x] No unnecessary native dependency introduced

## Outcome

SaintFlick is already an app-quality, installable product through its PWA. The right call is to keep that simplicity until native capabilities, not the wish for an app-store icon, create a real reason to add a native runtime.

## References reviewed

- [Capacitor: installation requirements](https://next.capacitorjs.com/docs/next/getting-started)
- [Capacitor: configuration and production caveats](https://next.capacitorjs.com/docs/next/config)
- [Capacitor: development workflow](https://next.capacitorjs.com/docs/next/basics/workflow)
- [Apple App Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- [Google Play: minimum functionality policy](https://support.google.com/googleplay/android-developer/answer/9898783)
- [PWABuilder documentation](https://docs.pwabuilder.com/)
