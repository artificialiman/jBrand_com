# BCM Homes — Context Dossier
**For: any agent or collaborator picking up this project cold**
**Companion docs:** `01-DESIGN-SYSTEM.md` (tokens/rationale), `02-CAD-LIBRARY.md` (component specs)
**Owner: Manchi**
**Status: pre-build — concept, story, and design system are settled; no code written yet**

---

## 1. What this is

BCM Homes is a rental marketplace launching in **Calabar and 5–6
neighbouring LGAs** (Cross River State) — annual leases, short-lets,
studios, and event-space rentals, all in one product. Its structural
thesis, stated plainly: **the platform is the only party either side is
allowed to talk to.** Tenants never contact landlords/agents directly;
all communication routes through BCM. This is a deliberate differentiator,
not a limitation — see §4 for why this matters against the competitive
field.

This document exists so a new agent (human or AI) can read start-to-finish
and understand the current state of the concept — including which ideas
were tested against real market research and why they held up — without
re-deriving anything from chat history.

---

## 2. Core roles (from original structure doc)

- **Admin (BCM internal):** platform control, approves users/listings,
  assigns verification agents, manages disputes, sees analytics — AND
  (new, see §6) runs the moderation/broadcast desk for citizen condition
  reports.
- **Property Partner:** landlords and listing agents collapsed into ONE
  role/dashboard, deliberately — no separate account types. Uploads
  listings, submits NIN/BVN identity verification. Personal contact info
  hidden from public users.
- **Tenant:** browses, saves, requests inspections, books — chats only
  with BCM Support, never the partner.
- **BCM Verification Agent:** physically inspects properties. (Flagged
  gap from the original doc: this role isn't listed as a "core role"
  alongside the other three, only appears in the workflow section — still
  unresolved whether it needs its own formal account type or is Admin
  staff wearing a different hat. Revisit before build.)
- **Trusted Fellow** (new role, emerged from this conversation — see §6):
  a person (could be a tenant, a local resident, not necessarily staff)
  who performs minimal-action condition reports and can contribute to a
  listing reaching hotspot tier through vetting/corroboration. Needs
  formal definition — is this a role with its own account state, or just
  a trait any verified user can exercise once they've built enough
  activity? **Open decision — flag before building the reporting system.**

---

## 3. Original spec items (from BCM_Homes_Structure.docx — still standing)

- Verification workflow: upload → pending queue → Admin assigns agent →
  physical inspection (photos, location, condition report, doc
  confirmation) → Admin approves/rejects/requests correction → listing
  shows "Verified."
- Badge tiers for Property Partners: Bronze (1–5 verified listings),
  Silver (6–20), Gold (21+) — auto-awarded. **Design note:** replace the
  🥉🥈🥇 emoji treatment with a custom mark before production (see
  `01-DESIGN-SYSTEM.md` §7). Open question carried over: is the listing
  count cumulative-ever or active-at-once? Not yet resolved.
- Communication matrix: strict hub-and-spoke through BCM. No
  Tenant↔Partner, no Tenant↔Agent direct contact, ever.

---

## 4. Competitive landscape (researched — see chat log for full citations)

**Three tiers exist:**
1. **Direct Nigerian competitors** (ClearRent, RentPal NG, EzyRent,
   SmartRent Naija, RentQuarters, Krent, NaijaStay) — nearly all converge
   on identical hero copy ("verified," "trusted," "no fraud"). This tier
   is visually generic and the word "verified" is fully devalued across
   it. **ClearRent is the one true philosophical opposite of BCM** — it
   markets *removing* the agent/middleman as a selling point, where BCM's
   whole thesis is mandatory intermediation. This contrast is worth owning
   visually, not hiding.
2. **Global category leaders** (Airbnb primarily) — set the visual grammar
   everyone in tier 1 unconsciously copies (verification badges near
   profile photos, photo-first cards, single restrained shadow tier,
   trust signals surfaced at decision points). Airbnb is a legitimate
   reference for restraint and photography-first design, NOT for its
   playful/gamified Superhost badge language, which reads too soft for
   BCM's register.
3. **Structural twins** — the real playbook:
   - **NoBroker (India)** is the closest working precedent for BCM's
     entire model: platform-performed physical verification plus
     algorithmic checks. Important caveat: NoBroker's own terms admit its
     "verified" label is algorithm-based, not a guarantee of physical
     confirmation — BCM's actual physical-inspection-plus-crowd-
     corroboration model (§6) is a STRONGER trust claim and the design
     should say so plainly rather than importing NoBroker's now-hedged
     "verified" language.
   - **Property24 Kenya** is the cautionary tale: a reviewer flagged it as
     having no moderation and no way to report a listing, calling it "an
     open invitation to scammers." BCM's Admin-moderated reporting loop
     (§6) is explicitly the fix for this exact failure mode.

**Supporting infrastructure landscape** (vertical stack BCM would plug
into, not competitors):
- **Identity/KYC:** Smile ID, Youverify, Kora, NUBAN — mature Nigerian
  NIN/BVN verification APIs. BCM should NOT build ID verification
  in-house; this is a build-vs-buy decision resolved toward buy. Note:
  none of the cheap-tier options include selfie/liveness matching by
  default — Youverify's fuller flow does. Worth deciding whether BCM's
  "Verified" tier requires liveness or just document-matching, since that
  changes cost per verification materially.
- **Payments/escrow:** Paystack, Flutterwave (local trust + lower fees),
  plus dedicated escrow-as-a-service patterns (locked funds, dispute
  window, evidence upload, controlled release) and Nigeria-specific escrow
  product Payluk. BCM's payment UI should use escrow-status language
  (held/disputed/released) rather than plain checkout language.
- **Property-management back office:** Buildium, AppFolio, Yardi (Admin
  dashboard reference), zInspector / Buildium's mobile inspection app
  (Agent field-capture reference — mobile-first, photo-heavy, assumes
  poor connectivity).

---

## 5. The amenities differentiator — solar/battery rental fleet

**Confirmed as genuine market white space, not just an underused
feature.** Nigerian grid supply averages under 12 hours/day in most
residential areas — backup power is the PRIMARY power source, not a
supplement. Every competitor treats "generator/inverter available" as a
passive listing filter. None sell power infrastructure as a bundled,
financed product tied to a specific rental.

**The actual mechanic (Manchi's addition, sharper than the original
"premium package" framing):** BCM owns a fleet of solar units and larger
battery banks and **wheels them to a tenant on request** — solving the
exact problem that traps DIY solar buyers in Nigeria today (a documented
case: a Lekki renter lost over ₦1M in solar-equipment value negotiating
fixture-vs-property disputes with his landlord when he moved out).
Because BCM owns the unit, it's rented and retrieved, not purchased —
zero of that friction. This also makes "power backup available" a live,
sellable attribute of a specific listing rather than a static checkbox.

- Premium package framing: available with warranty and hire-purchase
  options.
- Two real SKUs, not one generic "power" product: **solar unit** OR
  **larger battery bank** (for units without good sun access, or needing
  bigger continuous draw).
- Positioned as its own card type in the feed (see `02-CAD-LIBRARY.md`,
  Amenity Card) — NOT a spec line on a property listing, NOT a modal.
  Reasoning: light/power anxiety is universal across Calabar, independent
  of which specific house someone picks, so it deserves its own narrative
  beat in the feed rather than being buried in a property's checkbox list.
- Artisan/helps partnerships (plumbers, electricians, cleaners, house
  help) should work the same way — **implicit infrastructure that comes
  with the property**, not a separate services marketplace tab the tenant
  has to go looking for. Not yet designed in detail — flagged for a
  future pass once the amenity-card pattern is validated with the solar/
  battery case.

---

## 6. The reporting/hotspot system (emerged this conversation — core mechanic)

This is the single most structurally important new idea in the project.
Read carefully before touching the feed or Admin build.

**The loop:**
1. Anyone in the coverage area performs a **minimal action** (one or two
   taps, preset chips — "power's out," "network's slow," "bus is late" —
   see `02-CAD-LIBRARY.md` Report Action component) reporting a live
   condition.
2. The report routes into a **chat-style queue that goes to Admin** —
   Admin verifies/moderates before anything broadcasts. This is the
   explicit fix for the Property24-Kenya failure mode (§4) — no
   unmoderated crowd claims ever reach other users directly.
3. Once verified, Admin **broadcasts** it — it surfaces as a live
   condition notification (see hierarchy rule below).
4. The reporter earns a **private shimmer accent on their own profile
   activity** — Register-B signature motion, one-time per action, NOT a
   public leaderboard number (deliberately — a public leaderboard invites
   gaming the system with fake reports for status; a private-only reward
   avoids that risk while still delivering the dopamine hit).

**Listings, not zones, are what carry trust tiers.** A "hotspot" is a
*specific listing* that has been either:
- vetted by a single **trusted fellow**, OR
- **independently corroborated by multiple fellows**

This is a stronger, human-confirmed trust claim than any competitor in
tier 3 offers (see NoBroker caveat, §4) — worth stating in-product,
without words, purely through the hotspot shimmer tier (see
`01-DESIGN-SYSTEM.md` §5).

**Notification hierarchy — hard rule, not a preference:** live condition
reports (grid/network/bus/bank-speed) must ALWAYS display less
prominently than listing alerts (a hotspot near you, a saved search
match). See `02-CAD-LIBRARY.md` Notification Chip component for the exact
visual treatment. If a future build makes these visually equal weight,
that is a regression against this spec, not a valid alternative.

**Open decisions not yet resolved — flag before building:**
- Is "Trusted Fellow" a formal role/account state, or an emergent trait
  any sufically-active verified user can exercise? (See §2.)
- What's the actual moderation SLA/workflow for Admin's queue — real-time
  chat triage, or batched review? Not yet discussed.
- Gaming resistance beyond "no public leaderboard" — e.g., rate-limiting
  reports per user/day, requiring account verification before a report
  counts toward hotspot corroboration. Not yet designed.

---

## 7. The feed — narrative logic (not yet built, structure agreed)

**The core insight:** BCM's feed does not optimize for comparison
(grid/Zillow-style) or geography (map/Airbnb-style) or impulse-discovery
(TikTok-style-for-its-own-sake). It optimizes for **trust-qualification,
one property at a time** — because the real anxiety BCM is solving is "is
this place real, can I trust it," sharper than any competitor faces
because of Nigeria's specific fraud environment.

**Landing experience:** the user is asked, once, in plain conversational
terms — "where would you like to be closest to?" (work, school, market,
family, whatever THEY say). BCM silently converts that into 30-minute
isochrons (walking / driving / bus) against every listing. This
replaces search/filter UI entirely for the default experience — **the
priority question IS the onboarding, and the shimmer IS the search
result.** No visible filter bar, no radius slider.

**Primary surface:** full-bleed, one property per screen, vertical swipe
(structurally like a Reels feed, but the "next" gesture is driven by
trust-evaluation, not boredom/desire). This gives the trust-tier shimmer
(§6, `01-DESIGN-SYSTEM.md` §5) room to actually play without competing
against a dozen other badges in a grid.

**Amenity cards (solar/battery, §5) are their own beat in the same
scroll** — not attached to any specific property.

**Rental-mode plurality:** annual / short-let / studio / event-space all
live in the same feed. Each has a different mental model (annual =
inspection-heavy commitment; short-let = closer to instant-book; event =
venue-for-hours, different pricing/availability logic entirely). Not yet
resolved how these differ in the browsing flow itself — currently only
resolved at the card-tag level (`02-CAD-LIBRARY.md`, Rental-Mode Tag). A
future pass should decide whether mode is a filter the user sets once
(closer to a dropdown they set before seeing the feed at all) or whether
all four modes genuinely interleave in one continuous scroll.

**Isochron engineering — real-world constraint, stated plainly:**
- Driving-time isochrons: can likely be computed from a standard
  routing API (Google Distance Matrix or OSRM/Mapbox on OSM data) — Calabar
  has decent road coverage for a state capital.
  Nigeria's road network runs through OpenStreetMap; anyone can extract
  and rebuild routing from it, but secondary-city street-level density on
  OSM is not guaranteed and should be checked before assuming
  walking-isochron accuracy.
- **Walking and bus isochrons are the real risk.** There is no GTFS-style
  transit feed for Calabar's local bus/keke system, so live routing-engine
  computation isn't possible for these modes at launch. Recommended path:
  launch these as **crowd-estimated**, openly labeled as such, using the
  same reporting mechanic as §6 (someone reports "15 min bus ride from X
  to Y," gets corroborated by others, becomes trustworthy over time same
  as any other crowd-verified fact on the platform). This reuses the
  trust-system architecture rather than requiring separate transit-data
  infrastructure — consistent with the platform's overall "ground truth
  from people, moderated by humans" model.

---

## 8. House style / working conventions (carried over from Manchi's
broader Studi054/UTMEDaily ecosystem — useful defaults, not mandates)

- HTML/CSS-first, browser-to-print pipeline preferred over native document
  formats when layout control matters, in adjacent projects — likely not
  directly relevant to BCM's app-shaped product, but the underlying
  preference for hand-controlled layout over template abstraction carries
  over.
- Communication style: terse, directive, execution-over-explanation.
  Discuss big/ambiguous decisions in plain language BEFORE building;
  concrete scoped asks get built immediately. (See working-style manual
  from the adjacent TCC report-page project — same collaborator, same
  default process.)
- Decisions that will recur should be written down as durable rules with
  their reasoning attached (this document is written in that spirit).
- BCM Homes is explicitly a SEPARATE brand identity from the TCC/
  UTMEDaily/Gracefield school-software side of Manchi's business — do not
  cross-pollinate visual language (see `01-DESIGN-SYSTEM.md` §7).

---

## 9. Summary for a new agent picking this up

You're designing/building a rental marketplace for Calabar + surrounding
LGAs, covering annual/short-let/studio/event rentals, where the platform
is the sole intermediary between tenants and property partners. Trust is
the entire product — communicated through a three-tier shimmer system
(plain/verified/hotspot) rather than badges or words, with hotspot status
earned through human vetting/corroboration, not algorithms alone. A
citizen-reporting loop feeds live condition data (power/network/transit)
through Admin moderation before broadcasting, doubling as the mechanism
that eventually produces trustworthy walking/bus travel-time data where
no formal transit data exists. BCM also rents out a physical fleet of
solar units and battery banks directly tied to listings — solving a real,
documented Nigerian renter pain point that no competitor addresses. The
design system (`01-DESIGN-SYSTEM.md`) and component library
(`02-CAD-LIBRARY.md`) translate all of this into a warm, Calabar-sourced,
restraint-first visual language — signature motion reserved for five
named conversion moments, everything else quiet. Feed structure, sketch,
and several open role/moderation questions (§2, §6, §7) are the next
things to resolve.
