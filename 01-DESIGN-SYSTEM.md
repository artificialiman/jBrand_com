# BCM Homes — Design System & Style Guide
**Version 1.0 — Calabar Launch**
**Companion docs:** `02-CAD-LIBRARY.md` (component specs), `03-AGENT-CONTEXT.md` (project brief for collaborators)

---

## 0. What this system is for

BCM Homes is a trust-brokered rental marketplace launching in Calabar and
5–6 neighbouring LGAs. The product's entire competitive advantage is
**trust that is witnessed, not asserted** — every visual decision in this
system exists to make verification *visible as an event*, not a label.

This is not a SaaS dashboard system and not a consumer social-feed system.
It borrows discipline from both and belongs to neither. The house reference
point is: **a well-made physical object from Old Calabar** — weighted
brass, aged timber, river clay, carnival gold used sparingly — rendered
with the restraint of a documentary, not the shine of a fintech app.

**The one rule everything else derives from:**
*Show, don't tell. If a word can be replaced by a witnessed moment, replace it.*

---

## 1. Color

Named, not generic. Every color is drawn from an actual material or place
in Calabar — this is deliberate; it is the thing competitors (Property24,
ClearRent, generic green-checkmark "Verified" badges) cannot copy without
copying the city itself.

| Token | Hex | Source / referent | Use |
|---|---|---|---|
| `--clay` | `#8A5A3B` | Riverbank laterite earth | Primary background warmth, section dividers |
| `--clay-deep` | `#5E3B26` | Wet clay, shadow side | Text on light backgrounds, deep UI chrome |
| `--brass` | `#B8873D` | The governor's bell, old ironwork trim | Primary accent — verification, CTA weight |
| `--brass-bright` | `#D9A94E` | Brass in direct sun | Hotspot-tier shimmer highlight only — never a flat fill |
| `--palm` | `#2F4A3C` | Mangrove / rainforest canopy | Secondary accent, success/confirmed states |
| `--palm-deep` | `#1C2E25` | Canopy shadow | Dark-mode base, night-mode chrome |
| `--river` | `#7C948C` | Calabar River under cloud | Neutral-cool, disabled states, quiet dividers |
| `--carnival` | `#C43B2F` | Calabar Carnival costume red | Reserved exclusively for live/urgent notification dot — never decorative |
| `--linen` | `#F1E9DC` | Sun-bleached wall plaster | Page background (light mode) |
| `--ink` | `#241C15` | Charcoal / soot on old timber | Primary text |

**Hard rule:** `--carnival` red is the only color permitted for the live
condition-notification dot (§6). If it appears anywhere else, it stops
meaning "this is a live report" and the whole notification language breaks.
Guard this like a fire alarm's color — one meaning, no exceptions.

**Hard rule:** `--brass-bright` never appears as a static fill. It only
exists inside the hotspot shimmer keyframe (§5). A designer reaching for
it as a "highlight color" elsewhere is a sign the system is being misused.

### Dark mode
Dark mode is not an inverted light mode — it's `--palm-deep` as base with
`--linen` text and `--brass` accents held at slightly lower saturation
(reads as "verandah at night," not "app in dark mode").

---

## 2. Typography

Two typefaces, one utility face. No more.

| Role | Face | Why |
|---|---|---|
| **Display** (headlines, the one word a screen needs) | A humanist serif with some ink-trap character — e.g. **Fraunces** (variable, has a "soft" optical setting that reads warm rather than formal) | Carries the "Old Residency ledger" feeling without going full broadsheet-Times. Used at LARGE sizes only, rarely more than 3–5 words per screen. |
| **Body / UI** | **Inter** or **General Sans** at standard weights | Gets out of the way. Nearly all copy on this product is short (see §0) so body type mostly renders labels, not paragraphs. |
| **Utility** (data, timestamps, badge microcopy, prices) | **JetBrains Mono** or **IBM Plex Mono**, small size, tabular figures | Anything numeric — price, minutes-away, kVA rating, timestamp — sits in mono. This is the one place the system borrows a technical register on purpose: numbers should read as *measured facts*, not marketing copy. |

**Type scale** (rem, 16px base):
`48 / 32 / 24 / 18 / 16 / 14 / 12`
Display face only ever appears at 48/32/24. Below that, everything is body
or utility — never a small serif caption. Small serif reads as decorative;
this system has no room for decoration.

**Rule:** if a screen needs more than one display-face headline, that's a
signal the screen is doing two jobs and should split.

---

## 3. Layout

- **8px base spacing grid.** Section-level spacing steps at 64px, matching
  the restraint (not airiness) of the Airbnb reference — dense enough that
  a feed feels alive, not gallery-empty.
- **Single shadow tier**, used sparingly: `0 1px 2px rgba(36,28,21,0.06), 0 4px 12px rgba(36,28,21,0.08)`.
  Never stack a second shadow tier for "more important" cards — importance
  is carried by the shimmer system (§5), not elevation.
  border-radius: one value system-wide — `12px` for cards, `8px` for
  controls, `999px` (full pill) only for status badges and the shimmer
  chip. No in-between radii.
- **Full-bleed vertical primary surface** for the feed (see `03-AGENT-CONTEXT.md`
  §Feed for the narrative reasoning) — the grid/dashboard layout is reserved
  for Admin and Agent surfaces only, never for the Tenant-facing feed.

---

## 4. Motion — the house rule

> **Shimmer, not spectacle.** Every satisfying-motion decision in this
> system answers one question first: *is this a conversion/trust moment,
> or is this ambient chrome?* Only conversion moments earn expressive
> motion. Everything else gets the quietest possible feedback.

### 4.1 Two motion registers

**Register A — Ambient (default for almost everything)**
- Loading states: a plain neutral shimmer sweep, `--river` at low opacity,
  1.2s ease-in-out, no color shift. This is the "something real is
  arriving" cue — quiet, expected, forgettable.
  <br>
  *This is the ONLY motion most of the interface should ever use.*

**Register B — Signature (conversion/trust moments only)**
Reserved exclusively for these five moments, named explicitly so no
agent invents a sixth without checking:
1. Becoming an agent (identity/role upgrade)
2. Verifying a listing (agent action)
3. Renting an amenity (solar/battery unit — the "utility beat" card)
4. Sharing an experience (review/testimonial submission)
5. A listing crossing into hotspot tier (§5)

These get the fuller, slower, weightier motion — a settle-with-mass
easing curve (`cubic-bezier(0.16, 1, 0.3, 1)`, ~600–900ms), not a bounce,
not a confetti burst. Think: a bank vault door closing, not a slot
machine. Satisfying because it's *substantial*, not because it's *fast*.

**Never:** motion on hover for its own sake, animated numbers ticking up
just to feel alive, parallax, or any effect that fires on page load
without the user having done anything. If it doesn't correspond to one of
the five moments above, it's ambient-only.

---

## 5. The shimmer system (core signature element)

Three tiers, escalating in both **color** and **motion duration/richness** —
this is the system's single signature element per the frontend-design
process (one bold thing, quiet everywhere else).

| Tier | Trigger | Color | Motion |
|---|---|---|---|
| **Plain** | Unverified listing, default loading state | `--river` at 8% opacity | 1.2s linear sweep, one pass, stops |
| **Verified** | BCM-agent physically inspected | `--brass` at 35% opacity | 1.8s ease sweep, loops twice on first view then settles to static badge |
| **Hotspot** | Vetted by a trusted fellow, or independently corroborated by multiple fellows | `--brass-bright` gradient sweep with a faint warm bloom (box-shadow pulse, not glow-for-glow's-sake) | 2.6s slow ease, continuous but at low duty-cycle (visible ~40% of the loop, quiet the rest) — reads as a "living" surface, not a strobing sticker |

**This IS the verification story, told without words.** A user scrolling
the feed never reads "Verified" — they feel a house glow at them
differently than its neighbour, and that difference alone is the entire
trust argument. See `03-AGENT-CONTEXT.md` for the narrative reasoning.

**Isochron overlay:** when a listing falls inside the user's stated
30-minute priority zone (walk/drive/bus), it shimmers *regardless of its
trust tier* — this is a fourth, independent shimmer trigger, and it should
be visually distinguishable from the trust-tier shimmers (a cooler-toned
`--palm` sweep rather than `--brass`) so "this is close to what you care
about" never gets confused with "this is trustworthy." Two separate
truths, two separate colors, both wordless.

---

## 6. Notification hierarchy (strict priority order)

Per the explicit instruction: live condition reports (grid/bandwidth/
traffic/bank-speed) must always read as **less prominent** than listing
alerts. This is a hard visual hierarchy, not a suggestion:

1. **Listing alerts** (a hotspot near you, a saved search matched, an
   inspection completed) — full-weight notification, `--brass` accent,
   sits in the primary notification surface.
2. **Live condition reports** (power, network, bus wait time, bank
   congestion) — smaller, quieter, `--river`-toned chip, no persistent
   badge count, auto-dismisses faster. Never uses `--carnival` red unless
   Admin has flagged something urgent (e.g., a safety report) — see hard
   rule in §1.

If a future screen makes these look equally weighted, that's a bug against
this system, not a valid alternate treatment.

---

## 7. Iconography & imagery

- No emoji medal icons (🥉🥈🥇) for partner tiers in production — replace
  with a single custom mark family (a brass-line badge shape that gains a
  second/third concentric ring per tier), consistent with the "Old
  Residency ledger" register. Emoji reads as a placeholder, not a brand.
- Photography over illustration wherever possible — this system trusts
  real inspected photos to carry weight the way Airbnb's professional
  photography program does, not iconography.
- The TCC/UTMEDaily ecosystem's dark-glass aesthetic (from `gracefield.css`
  and the Testy repo reference) is explicitly NOT reused here — BCM Homes
  is a distinct brand family from the school-software side of the
  business and should not visually resemble it.

---

## 8. What this system deliberately refuses

(Stated so no future agent "fixes" these as oversights.)

- No numbered-step markers (01/02/03) unless a flow is a genuine literal
  sequence — most of BCM's screens are single-moment, not multi-step.
- No stacked shadow tiers, no glassmorphism, no gradient-mesh backgrounds.
- No animated counters/ticking numbers as ambient decoration.
- No cream-background/terracotta-serif combination pulled from generic
  AI-design defaults — this palette is Calabar-sourced and named, not a
  stock warm palette (see §1 sourcing column).
- No word "Verified" set in large display type as a hero element — the
  shimmer tier communicates this; the word is a fallback for
  accessibility/screen-readers only, never the primary signal.
