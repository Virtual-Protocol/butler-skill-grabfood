# Changelog

## 1.0.0

- **GrabFood as its own skill**, built on `butler-app-checkout`
  (`requires.skills`), so a "GrabFood" request finds it: the generic skill has no
  food keyword, and on 2026-10-07 a butler searching the hub for GrabFood found
  nothing and fell back to Grab's website, which wants a login before it will
  search a location.
- Grab's own screens, as seen in the Malaysian app that day: the sign-in labels,
  the curly-apostrophe `DON’T ALLOW`, Food → search → "See all N outlets", the
  three ways a branch says it isn't delivering, and sizes listed as separate
  items (`M-Milk Tea`).
- Checkout, approval and the Place order tap stay in `butler-app-checkout`.
