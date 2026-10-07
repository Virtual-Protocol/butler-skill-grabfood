# butler-grabfood

Order food or drinks on GrabFood in the Grab phone app: find the shop, pick a
branch that is actually delivering, read the menu, and build the basket. The
checkout, the owner's approval and placing the order are
[`butler-app-checkout`](https://github.com/Virtual-Protocol/butler-skill-app-checkout)'s —
this skill declares it in `metadata.butler.requires.skills`, so the hub installs
it first, and hands over at that skill's checkout step.

It exists for two reasons, both measured on 2026-10-07 on a local butler ordering
KOI Thé in Kuala Lumpur:

- **Discovery.** `butler-app-checkout` has no "grabfood" or "food" keyword, so
  the butler's hub search for GrabFood came back empty and it tried Grab's
  website instead.
- **Speed.** Without Grab's path written down, the butler scrolled the promoted
  feed for the shop, opened closed branches one by one, and handed labelled
  screens to the slower `do` agent. Each run took about 25 minutes before
  reaching the basket.

Every label in `SKILL.md` was read off the Malaysian app that day. Grab changes
its app; when a label drifts, update it here and bump the version.

One Butler skill, published by the
[Butler skill hub](https://github.com/Virtual-Protocol/butler-skills): the hub's
`skills.json` lists it by name, repo and ref.

- `SKILL.md` — the playbook (see the hub's
  [SKILL_STANDARD.md](https://github.com/Virtual-Protocol/butler-skills/blob/main/SKILL_STANDARD.md))
- `CHANGELOG.md` — one entry per version; every change bumps `version` in SKILL.md

Validate locally:

```sh
curl -sSLO https://virtual-protocol.github.io/butler-skills/tools/validate.py
python3 validate.py --standalone .
```
