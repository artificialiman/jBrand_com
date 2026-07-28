# BCM Homes — Component (CAD) Library
**Companion to:** `01-DESIGN-SYSTEM.md` (tokens/rationale), `03-AGENT-CONTEXT.md` (project brief)

Concrete, buildable component specs. Every value here derives from the
tokens in `01-DESIGN-SYSTEM.md` — do not introduce a new color, radius,
or timing value here without adding it to that file first.

---

## Component: Listing Card (feed primary surface)

**Shape:** full-bleed, one per viewport in the vertical feed (see
`03-AGENT-CONTEXT.md` §Feed for why this is the surface, not a grid).

```
┌─────────────────────────────────────┐
│                                     │  <- photo, full-bleed,
│                                     │     inspected/verified photos
│         [property photo]           │     only — no stock imagery
│                                     │
│  ◐ shimmer plays here on mount ─────┼──  (tier per §5 of design system)
│                                     │
├─────────────────────────────────────┤
│ ₦ price · mono utility face         │
│ location line · body face, 1 line   │
│ [mode tag: annual/short-let/        │
│  studio/event]                     │
└─────────────────────────────────────┘
```

**Behavior:**
- Shimmer tier plays automatically on card mount (first glance, per
  explicit instruction — never gated behind a tap for the trust shimmer).
- Isochron shimmer (palm-toned, §5) is an independent overlay — a card can
  show BOTH a trust shimmer (brass family) and an isochron shimmer (palm)
  simultaneously if both are true. They must never blend into a single
  color; render as two distinct passes so each truth stays legible.
- No text badge reading "VERIFIED" as the primary signal. A small
  screen-reader-only label carries the equivalent meaning for
  accessibility (`aria-label="BCM verified listing"` /
  `"Hotspot: vetted by trusted fellows"`).
- Swipe up = next card. Swipe down = previous. No "like" heart icon —
  saving happens via a held-press (mirrors the weight of a real decision,
  not a disposable like).

**States:**
| State | Visual |
|---|---|
| Loading | Register-A ambient shimmer (`--river` 8%, 1.2s, one pass) fills the photo area as a skeleton |
| Plain | No shimmer after load, static |
| Verified | Brass shimmer per §5, settles to a small static corner mark after 2 loops |
| Hotspot | Brass-bright shimmer per §5, continuous low-duty-cycle |
| In isochron | Palm-toned shimmer pass, independent of trust tier |

---

## Component: Amenity Card (solar/battery rental — its own card type)

Per explicit instruction: this is its OWN card in the feed stream, not a
line item on a property card, and not a modal. It interrupts the property
feed the way a distinct feed beat would (structurally similar to how an
editorial break interrupts a product feed elsewhere — but this is utility,
not an ad).

```
┌─────────────────────────────────────┐
│  [photo: the physical unit itself,  │
│   not a stock icon of a battery]    │
│                                     │
│  "No light where you're moving?"    │  <- the only sentence this
│                                     │     card needs; the rest is
│  ₦ /week · mono                     │     visual (see §0 house rule)
│  [ Rent it delivered ]  <- Register-B│
│    motion on tap (one of the five   │
│    named conversion moments)        │
└─────────────────────────────────────┘
```

**Behavior:**
- Tapping "Rent it delivered" triggers Register-B signature motion
  (settle-with-mass, 600–900ms) — this is one of the five named
  conversion moments in the design system.
- Options surfaced on expand: solar unit vs. larger battery bank (per
  "solar OR just bringing our bigger batteries" — both are real SKUs,
  not one generic "power" product).
- Warranty / hire-purchase terms live one tap deeper — never crammed
  onto the card face. The card's job is the single emotional hook, not
  the financing terms.

---

## Component: Trust Shimmer (shared visual primitive)

Used by: Listing Card, Partner profile badge, Agent profile badge,
Testimonial card.

```css
/* Register A — Ambient / Plain loading */
.shimmer-plain {
  background: linear-gradient(
    100deg,
    transparent 30%,
    rgba(124, 148, 140, 0.08) 50%,  /* --river at 8% */
    transparent 70%
  );
  animation: sweep 1.2s ease-in-out 1;
}

/* Register B — Verified */
.shimmer-verified {
  background: linear-gradient(
    100deg,
    transparent 25%,
    rgba(184, 135, 61, 0.35) 50%,   /* --brass at 35% */
    transparent 75%
  );
  animation: sweep 1.8s ease-in-out 2;
}

/* Register B — Hotspot */
.shimmer-hotspot {
  background: linear-gradient(
    100deg,
    transparent 20%,
    rgba(217, 169, 78, 0.55) 50%,   /* --brass-bright at 55% */
    transparent 80%
  );
  box-shadow: 0 0 24px rgba(217, 169, 78, 0.15); /* faint bloom, not glow-for-glow's-sake */
  animation: sweep 2.6s ease-in-out infinite;
  animation-timing-function: cubic-bezier(0.45, 0, 0.55, 1); /* long dwell, quiet return */
}

/* Isochron overlay — independent of trust tier, palm-toned */
.shimmer-isochron {
  background: linear-gradient(
    100deg,
    transparent 30%,
    rgba(47, 74, 60, 0.30) 50%,     /* --palm at 30% */
    transparent 70%
  );
  animation: sweep 1.8s ease-in-out 1;
}

@keyframes sweep {
  from { background-position: -200% 0; }
  to   { background-position: 200% 0; }
}
```

**Reduced-motion:** all four variants collapse to a static tinted border
(same color, no animation) when `prefers-reduced-motion` is set — the
color hierarchy still communicates tier; only the motion is removed.

---

## Component: Notification Chip (condition reports — deliberately quiet)

```
┌──────────────────────────┐
│ ○ Power: 4hrs today       │   <- --river tone, small, no badge count,
└──────────────────────────┘      auto-dismiss ~6s, sits BELOW listing
                                   alerts in stack order always (§6)
```

vs.

```
┌──────────────────────────┐
│ ● Hotspot near you!       │   <- --brass, full notification weight,
└──────────────────────────┘      persists until dismissed
```

**Hard rule reminder:** the `--carnival` red dot only ever appears on an
Admin-flagged urgent/safety report. Never on routine grid/network/traffic
chips, even a bad one ("power's been out 12 hours") — severity is
communicated through copy and chip persistence, not by borrowing the
emergency color for routine bad news.

---

## Component: Report Action (the "minimal action" citizen-reporting entry point)

This is the interaction that feeds the whole condition-notification /
hotspot-corroboration system. Must be genuinely minimal — one tap plus
optionally one more, never a form.

```
[ tap: "Power's out" / "Network's slow" / "Bus is late" — preset chips ]
       → optional second tap: rough duration (chips: "just now" /
         "few hours" / "all day")
       → done. No text field required for the base case.
```

**Routing:** submission enters the Admin-facing chat/moderation queue
(see `03-AGENT-CONTEXT.md` §Reporting Loop) before it broadcasts. The
person who reported gets a private shimmer-accent on their own profile
activity (Register B, brief, one-time) — never a public leaderboard
number (see open decision log in `03-AGENT-CONTEXT.md`).

---

## Component: Rental-Mode Tag

Small pill, one per card, distinguishes the four transaction shapes.
Utility mono face, not display face — this is a fact label, not a
headline.

| Mode | Pill label | Color |
|---|---|---|
| Annual | `ANNUAL` | `--clay-deep` on `--linen` |
| Short-let | `SHORT-LET` | `--palm` on `--linen` |
| Studio | `STUDIO` | `--river` on `--linen` |
| Event space | `EVENT` | `--brass` on `--linen` |

No icon set for these yet — text-only pill is correct at MVP scope. Do
not invent icons for this table without a design pass; a mismatched icon
language here is a common way these systems drift.

---

## Open component work (not yet specified — flag before building)

- Admin moderation queue / broadcast chat UI — needs its own pass, likely
  closer to the "dense dashboard" register (§3 of design system) than the
  Tenant-facing feed register. Do not reuse feed-card shimmer language in
  Admin's own UI chrome — Admin sees raw data, not the shimmer story.
- Agent field-inspection capture flow (photos, condition report, doc
  confirmation) — mobile-first, likely closer to zInspector/Buildium's
  field-app register than the consumer feed. Needs its own component pass.
- Partner/Agent trust badge visual mark (replacing 🥉🥈🥇 placeholders) —
  flagged in design system §7, not yet drawn.
