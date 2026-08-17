# NameplateSCT

Nameplate-based scrolling combat text for World of Warcraft. Damage numbers float off the
nameplate of the thing you hit, styled how you want them, with per-school colors, crit
sizing and a handful of animations.

This fork restores functionality on **Midnight (12.x)**, where the addon previously disabled
itself. Everything from Vanilla through The War Within behaves exactly as before.

Download and unzip into your `World of Warcraft\_retail_\Interface\AddOns` folder, or grab it
from [CurseForge](https://www.curseforge.com/wow/addons/nameplate-scrolling-combat-text).

## Midnight (12.x)

Blizzard removed `COMBAT_LOG_EVENT_UNFILTERED` for addons in 12.0 — the same change that
made Details! and Plater drop their combat log parsers. NameplateSCT now reads damage from
`UNIT_COMBAT` instead, which reports what happened to each unit and hands back a unit token
directly, so numbers still anchor to the right nameplate.

**Works on Midnight:** damage numbers on nameplates, criticals, per-school damage colors,
misses/dodges/parries/absorbs, personal SCT, and every font, size, color, offset, strata,
variance and animation option.

**Not possible on Midnight:** `UNIT_COMBAT` carries no source and no spell id, so there is
no way to tell who dealt a hit or with which spell. That costs:

- **Source attribution** — numbers appear for *all* damage a target takes, not only yours.
  Solo this is invisible; in a group you will see other players' hits too.
- **Spell icons** — nothing to look an icon up by.
- **The spell filter** — the NPC filter still works. Both remain available on older flavors.
- **Overkill**, and the separate auto attack / ability animation split.

Options that depend on the missing data are hidden on Midnight rather than left as switches
that do nothing.

12.0 also introduced *secret* values: combat data addons are not allowed to read. When an
amount comes through secret it is still drawn, just unformatted — no truncation to `44k`, no
small-hit averaging, no absorb breakdown.

### Upgrading from an older version? Check your threshold first

Midnight squished damage numbers by roughly an order of magnitude. If you had
**Sizing Modifiers → Hide Hits Threshold** set to something sensible for The War Within
(say `200000`), it now sits above your biggest crit and hides *every* number, which looks
exactly like the addon being broken. Set it to `0` if nothing appears.

Worth checking at the same time: **Hide Small Hits**, and **Appearance/Offsets → Target
Strata** — `Background` draws the text behind your nameplates.

## Commands

- `/nsct` — open the options panel
- `/nsct debug` — dump raw combat events to chat, marking which fields the client is keeping
  secret, and stop after 40 of them. Useful when numbers do not appear and you want to know
  whether the addon is receiving anything at all.

## Supported flavors

| Client | TOC |
| --- | --- |
| Midnight / retail | `NameplateSCT.toc` |
| Mists of Pandaria | `NameplateSCT_Mists.toc` |
| Cataclysm | `NameplateSCT_Cata.toc` |
| Wrath of the Lich King | `NameplateSCT_Wrath.toc` |
| The Burning Crusade | `NameplateSCT_TBC.toc` |
| Vanilla | `NameplateSCT_Vanilla.toc` |

## Building from source

`Libs/` is not checked in. Releases are assembled by
[BigWigsMods/packager](https://github.com/BigWigsMods/packager), which pulls the libraries
listed in `.pkgmeta` and substitutes the version into each TOC. A bare clone dropped into
`AddOns/` will not load until those libraries are present.

## Credits

Originally by [mpstark](https://github.com/Mpstark/NameplateSCT), maintained by
[Justwait](https://github.com/Justw8/NameplateSCT). MIT licensed.
