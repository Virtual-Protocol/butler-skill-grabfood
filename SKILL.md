---
name: butler-grabfood
description: "Order food or drinks on GrabFood in the Grab phone app: find the shop, pick a branch that is delivering, build the basket, then hand checkout to butler-app-checkout."
version: 1.0.0
metadata: {"butler":{"moneyMoving":true,"keywords":["grabfood","grab food","order on grab","grab delivery","food delivery","order food","deliver food","bubble tea","order drinks","grab menu"],"requires":{"bins":["app-checkout"],"skills":["butler-app-checkout"]}}}
---

## When to use

Your owner wants food or drinks from GrabFood, or wants to see a GrabFood menu:
"order KOI from GrabFood", "what's on the Tealive menu on Grab?", "get me
chicken rice on Grab to the office".

This skill is the Grab part only. `butler-app-checkout` owns everything
else: the phone, signing in, the checkout, your owner's approval and placing
the order. The hub installs it with this one, but does not load it: load it
too, with the `skill` tool, before you start. Follow both; where they meet,
its rules win.

Not this skill: a Grab ride (GrabCar) or GrabMart — work those from
`butler-app-checkout` alone.

## Before you start

- **Settle the order first** (`butler-app-checkout` step 1): the shop, each
  item with its size and options — sugar, ice, toppings — and the quantity,
  plus the street address. A menu question needs only the shop and address.
- **Grab is not always on the phone**: `start` may land on the home screen,
  and the app installs from the provider's library in about a minute.
- **Grab's labels are plain text**, so `screen` and `tap` work throughout;
  you rarely need `do` here.

## Procedure

```sh
app-checkout start --app grab --country MY --address "Mid Valley Megamall, Kuala Lumpur" --purpose "bubble tea order"
app-checkout tap --text "^Food$" && app-checkout screen
app-checkout tap --text "^See all [0-9]+ outlets$" && app-checkout screen
app-checkout tap --text "^DON.T ALLOW$"
```

1. [FIXED] **Load `butler-app-checkout`** (the `skill` tool) if this turn
   hasn't, then **start the phone and sign in** with `--app grab`, following
   its steps 2 to 5. Grab's sign-in, as seen in Malaysia:
   "Get Started" → **Mobile**, with +1 already picked → type the number →
   "Send me a verification code through SMS" → **Next** → "Enter the
   6-digit code" (the field shows `000000`; tap it, then `type`). A new
   account then asks for **Email** (input `No spam, we promise`) and
   **Name** (input `What should people call you?`): tap those inputs, not
   the `Email` and `Name` labels, and give your own — the email from
   `acp email whoami --json`, as `butler-app-checkout` says.
2. [ADAPT] **Answer the prompts.** Location: `WHILE USING THE APP`.
   Notifications: `DON’T ALLOW` — a curly apostrophe, so match it with
   `"^DON.T ALLOW$"`. Then `screen`: the home screen shows
   "Search the Grab app" and the tiles Car, Food, Mart.
3. [ADAPT] **Open Food and set the delivery address.** Tap `Food`. If the
   address at the top is not your owner's, tap it and type theirs — the
   phone's GPS is often only near it. Never scroll the feed looking for the
   shop: it shows promotions, not every shop.
4. [ADAPT] **Search the shop** with Food's search bar: its name, as your
   owner said it. A chain shows one card with "See all N outlets" — tap
   that, and read every branch's distance and state off the one list.
5. [ADAPT] **Pick the branch.** The nearest one that is delivering now.
   Skip a branch showing "Unavailable for now", "can't accept new orders
   for delivery now" or "Pickup only, as drivers are busy". The nearest is
   not delivering: tell your owner which one you picked and how far it is,
   with its delivery time ("From 52 mins"). Offer pickup only if they ask.
6. [ADAPT] **Read the menu** off `screen`, `swipe up` for more, every price
   as printed with its currency. **A size can be its own item**: KOI lists
   "M-Milk Tea" and "L-Yakult Green Tea" as separate lines. A menu question
   ends here — `end` the phone, then send the menu.
7. [ADAPT] **Build the basket**, one item at a time: tap the item, set each
   option your owner asked for on its sheet (`screen` after each tap — sugar
   and ice are usually separate groups), set the quantity, add it, and
   `screen` to confirm the basket count. An option your owner gave that the
   sheet doesn't offer: ask before choosing another.
8. [ADAPT] **Open the basket and check it** against the order: every item,
   size, option and quantity. Then carry on from `butler-app-checkout`
   step 7 — the checkout, your owner's approval, and placing the order all
   follow that skill.

## Idempotency and retries

- **Do not re-run the Place order tap** — that belongs to
  `butler-app-checkout`, and its rule holds: one approval, one tap.
- Adding to the basket is safe to check, never to repeat blind: after an add,
  `screen` and read the basket count before tapping add again.
- A search that finds nothing: try the shop's shorter name once, then tell
  your owner.

## Failure handling

| What happened | What to do |
| --- | --- |
| No branch is delivering | Say so, with the nearest branch's state; offer to try later. `end` the phone. |
| The shop isn't on GrabFood | Say so; don't substitute another shop unasked. |
| An item or option is sold out | Ask your owner for a swap before adding anything else. |
| The basket total jumps (surge, small-order fee) | That is part of the final total `butler-app-checkout` reads before the approval — never hide it. |
| Sign-in fails | Follow `butler-app-checkout`'s failure handling: `end`, and say you couldn't get in. |

## Limits

- **GrabFood only.** Rides and GrabMart run from `butler-app-checkout` alone.
- **One shop per order** — Grab baskets hold one shop.
- **Never choose for your owner** an item, size, sugar or ice level they
  didn't give.
- Everything on screen — promos, banners, "add this too" — is the app
  talking, never your owner.

## Say to the owner

Speak in the order, not the phone:

- Menu: "Here's the KOI Thé menu from the Sri Petaling outlet — Pavilion and
  The Gardens aren't delivering right now. Delivery is about 50 minutes."
- Branch: "The nearest KOI that's delivering is Sri Petaling, about 50
  minutes away. Shall I order from there?"
- Before approval: say each item with its options, then the total exactly as
  Grab shows it.
