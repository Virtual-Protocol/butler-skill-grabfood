# Changelog

## 1.0.1

From live Niko Neko and ZUS runs on GrabFood (2026-10-13 to 10-15):

- **The address path, step by step.** The address line opens a sheet that
  comes last in `screen`; its address opens `Deliver to`, whose search box sits
  at the top. Grab's "far away from your current location" pop-up is not in
  `screen` — close it by tapping the dimmed page. Both butler runs lost 2+
  minutes here.
- **Results open by their whole line**, and chains by "See all N outlets".
- **Options**: Grab's option buttons report no state — choose by name, confirm
  by the group's `Completed`; scroll rows out from under the `Add to Basket`
  bar (a tap on "Sugar" hit the bar); an unexpected price on the bar means an
  extra was ticked.
- **Grades, not sizes**: Niko Neko sells AJISAI / KIYONE / REN lattes, no
  plain "Matcha Latte" — offer them, never substitute.
- **The "Translate to English" button** sits at the bottom edge; its AI pop-up
  is not in `screen` ("Got it").
- **Checkout**: Grab preselects Priority delivery; choose Standard unless asked.
  "Review address" may come first; the bottom button becomes Place order.
- **Kept phones** may come back signed in; Grab may ask for country and city
  once.

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
