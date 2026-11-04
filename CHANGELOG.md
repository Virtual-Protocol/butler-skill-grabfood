# Changelog

## 1.0.4

From DeepSeek and Sonnet runs on AWS staging (2026-11-04); Sonnet reached the
approval in 11.5 minutes, both lost the most time on Grab's address review:

- **The floor or unit, or "none", asked up front** with the instruction and
  the number — all before `start`, because a mid-checkout question idled a
  phone out (owner's call: ask when unsure about the order).
- **Ask about the order, never about the app.** Unit, instruction, a price
  that moved: ask, once. A switch's state or whether text landed: read
  `screen` — the owner can't see the phone.
- **Review address, as it behaves:** "Not applicable" flips by the switch
  beside it, not its label; the note box is under "Add instructions to help
  your driver", and a `0/255` counter means the typed note didn't land;
  Confirm does nothing until both are set. No instruction tapped "for now" —
  both runs tapped "Hand it to me" before the owner's.
- **Re-check delivery after the address.** Confirming it put Priority back
  (fee 8.80 for Standard's 6.30): read the fee line and tap Standard again.

## 1.0.3

From a GrabFood run on DeepSeek 4.1 Flash, AWS staging (2026-11-04), which
reached the approval but spent four minutes on Grab's address review (owner's
calls, 2026-11-04):

- **The driver instruction and a local phone number, asked up front.** Grab
  won't confirm `Review address` without a delivery instruction; the run
  tapped "Hand it to me" itself, then asked mid-checkout while the phone
  idled. Both are now settled before `start`, in the one ask: the
  instruction, and a local number the driver can call — the Grab account's
  number is the butler's own +1. The number goes into the note to the driver
  ("Call <number> on arrival") and nowhere else.
- **Card by default.** Payment is card unless the owner asks for cash,
  replacing 1.0.2's "ask when Grab offers both" and `butler-app-checkout`'s
  cash-first default on Grab. A card saved in Grab is used only when the
  owner says so; otherwise `butler-app-checkout`'s Paying by card.

## 1.0.2

From a GrabFood run on AWS staging (2026-10-28) that lost about six minutes
at checkout:

- **Standard delivery, read from the fee.** The selected delivery card is
  only a green border, which `screen` cannot show; the butler took nine
  screenshots and handed it to `do` for 2.5 minutes. Each option's price is
  on its row and the `Delivery fee` line shows the chosen one's, so that is
  the check. Standard's tap did not take on that run — then keep Priority
  and name it, with its fee, in the approval, rather than retry.
- **`Review address`**: check the pin is the owner's; fill only the unit,
  floor or driver note they gave. The run picked "Meet at lobby" itself.
- **Never choose a driver note** for your owner (Limits).
- **Cash or card, when Grab offers both** (owner's call, 2026-10-28): read
  the payment row and ask the owner which, once, before the checkpoint;
  only one offered, use it. Here rather than in `butler-app-checkout`,
  because not every app takes both.

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
