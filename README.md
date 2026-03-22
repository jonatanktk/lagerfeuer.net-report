# lagerfeuer.net – Domain Abuse Report

12 redirect chains recorded across two monitoring sessions, documenting political disinformation, affiliate traffic laundering, VPN social engineering, unsolicited adult content, and gambling advertising originating from or attributed to lagerfeuer.net.

| Metric | Count |
|---|---|
| Redirect chains | 12 |
| Tracking sessions | 2 |
| Threat categories | 6 |
| Shared infrastructure nodes | 13 |

## Threat Categories

| Category | Chains |
|---|---|
| Political disinformation | C2, C4, C5 |
| Affiliate traffic laundering | C1, C3 |
| VPN social engineering | C6, C7, C10 |
| Adult content (no consent) | C12 |
| Unsolicited gambling | C9 |
| Legitimate (mixed rotation) | C8, C11 |

## Report Sections

**Start here - Report Overview**
Findings summary, threat categories, and key reporting contacts.

**Chain Overview**
Summary table of all 12 chains, TDS architecture, and shared infrastructure map.

**Desktop Chains 1–5, 12**
Disinformation, affiliate laundering, and adult content via desktop sessions.

**Mobile Chains 6–11**
VPN social engineering, gambling, and legitimate mixed-rotation chains.

## Monitoring Sessions

| Session | Chains | Date/Time |
|---|---|---|
| Session 1 | Chains 1–11 | Thursday, 05 March 2026 · 20:00–21:00 CET |
| Session 2 | Chain 12 | Friday, 07 March 2026 · ~23:00 CET |

---

## Chain Summary

| # | Chain | Tracked | Device | Entry Domain | Final Destination | Threat Category |
|---|---|---|---|---|---|---|
| 1 | Chain 1 | 05.03.2026 | Desktop | lagerfeuer.net | alishopmart.com | Affiliate traffic fraud / Low-trust e-commerce |
| 2 | Chain 2 | 05.03.2026 | Desktop | xml-v4.pushub.net | nachrichtenanalyse-online.click | Political disinformation (Merz/Chrupalla) |
| 3 | Chain 3 | 05.03.2026 | Desktop | lagerfeuer.net | climamarket.com (via Kelkoo) | Affiliate traffic laundering |
| 4 | Chain 4 | 05.03.2026 | Desktop | xml-v4.pushub.net | nachrichtenanalyse-online.click | Political disinformation (Merz/Chrupalla) |
| 5 | Chain 5 | 05.03.2026 | Desktop | xml-v4.pushub.net | nachrichtenanalyse-online.click | Financial fraud (Krypto Reserve scam) |
| 6 | Chain 6 | 05.03.2026 | Mobile (sim.) | sumat-uah.com | primechain-track.com | Social engineering / VPN install prompt |
| 7 | Chain 7 | 05.03.2026 | Mobile (sim.) | lagerfeuer.net | primechain-track.com | Social engineering / VPN install prompt |
| 8 | Chain 8 | 05.03.2026 | Mobile (sim.) | theconsumersearch.com | gesundheitsvergleich-deutschland.de | Legitimate advertising (Bing/Yahoo) |
| 9 | Chain 9 | 05.03.2026 | Mobile (sim.) | plenalo8.com | 2-spinwinera11.com | Gambling affiliate (unsolicited) |
| 10 | Chain 10 | 05.03.2026 | Mobile (sim.) | press-to-see.com | NordVPN (Google Play) | Affiliate abuse / VPN install |
| 11 | Chain 11 | 05.03.2026 | Mobile (sim.) | travellookups.shopperbasics.com | airbnb.de | Legitimate advertising (Bing/Yahoo) |
| 12 | Chain 12 | 07.03.2026 | Desktop | xml-v4.pushub.net | darkteens.net | Adult content (unsolicited, no age gate) |

---

## Technical Architecture - TDS Pattern

The redirect infrastructure observed across these chains is consistent with a Traffic Distribution System (TDS) - a server-side routing layer that qualifies incoming visitors and distributes them to different offer endpoints based on real-time parameters such as device type, browser geometry, timezone, IP geolocation, and bot-detection score.

The TDS pattern is visible in lagerfeuer.net's entry behaviour (Chains 1, 3, 7):

1. **JavaScript bot detection** - a client-side fingerprinting script runs on page load
2. **JWT token issuance** - a cryptographically signed session token is generated and appended to a redirect URL, preventing replay by security scanners
3. **Visitor registration** - traffic is forwarded to an analytics layer (achel-xof.com / caish-djc.com / sumat-uah.com) that logs device fingerprint, browser geometry, GPU, timezone, and iframe/webdriver detection results
4. **Conditional routing** - qualifying traffic (non-bot, real browser, valid geometry) is forwarded to the active offer; non-qualifying traffic is dropped silently

This architecture is specifically designed to defeat automated abuse scanners: only real human users with real browsers, real screen sizes, and real GPU readouts pass the filter and reach the final destination.

```
lagerfeuer.net (TDS entry)
       │
       ├─ JS fingerprint + JWT
       │
       ▼
achel-xof.com / caish-djc.com / sumat-uah.com
  (visitor registration + bot filter)
       │
       ├──────────────────────────────────────┐
       ▼                                      ▼
click-for-preview.com              xml-v4.pushub.net / pornamigo
  (distribution hub)                 (push ad network)
       │                                      │
       ├─ alishopmart.com (C1)                ├─ nachrichtenanalyse-online.click
       │                                      │    ├─ Merz/Chrupalla (C2, C4)
       └─ primechain-track.com (C6,C7)        │    └─ Krypto Reserve (C5)
            └─ NordVPN Play Store (C10)       │
                                              └─ darkteens.net (C12, via tsyndicate)

lagerfeuer.net (direct, desktop, C3)
       └─ shopli.city → Kelkoo → climamarket.com
```

The three push notification ecosystems observed - Pushub, pornamigo, and beedirect - appear to operate as separate RTB layers that are accessed sequentially or through a traffic rotator.

---

## Threat Category Details

### Political Disinformation (Chains 2, 4, 5)

Three chains route through the Pushub push notification network to nachrichtenanalyse-online.click, a multi-campaign platform hosting political content and financial fraud offers. Chains 2 and 4 deliver a Merz/Chrupalla political narrative; Chain 5 serves a "Krypto Reserve" cryptocurrency offer from the same domain. The repeated delivery of the same content across multiple independent auction slots within a single monitoring hour is consistent with patterns observed in coordinated push-notification disinformation campaigns.

### Affiliate Traffic Laundering (Chains 1, 3)

Chains 1 and 3 originate directly from lagerfeuer.net. Chain 1 routes through a six-hop architecture typical of affiliate traffic washing, terminating at alishopmart.com (low-trust e-commerce). Chain 3 routes arbitraged traffic through shopli.city and dighlyconsive.com into the Kelkoo affiliate network - a legitimate European price-comparison service - potentially generating affiliate commissions on a genuine retailer (climamarket.com) without organic user intent.

### VPN Social Engineering (Chains 6, 7, 10)

Mobile visitors - both via direct navigation and via the click-for-preview.com distribution hub - are routed to primechain-track.com, a fake video player page prompting VPN installation. Chain 10 routes directly to the NordVPN listing on Google Play via an affiliate link (affsub=52381). The shared server IP 168.119.149.123 between primechain-track.com and press-to-see.com confirms a single actor operates both the social engineering page and the direct Play Store redirect.

### Adult Content Delivery (Chain 12)

Chain 12 starts at xml-v4.pushub.net with lo=live.pornamigo.com. The final destination URL contains ?host=live.pornamigo.com/filter?q=lagerfeuer, identifying lagerfeuer.net as a registered publisher on pornamigo.com. Adult content (darkteens.net) is delivered via the Pushub/pornamigo RTB network without age verification, age gating, or user consent.

### Unsolicited Gambling (Chain 9)

Chain 9 routes through the casino affiliate rotator plenalo8.com to 2-spinwinera11.com (SpinWin Era online casino), using Google PPC attribution parameters to obscure the true traffic source from the gambling operator.

### Legitimate Advertising - Mixed with Malicious Chains (Chains 8, 11)

Chains 8 and 11 are legitimate paid advertising placements (Bing/Yahoo) landing on a health supplement comparison site and Airbnb respectively. Their co-existence with malicious chains in the same push notification rotation generates real revenue and provides plausible cover against enforcement.

---

## Shared Infrastructure

| Domain / IP | Role | Chains |
|---|---|---|
| lagerfeuer.net (212.92.104.5 / 172.241.213.99) | TDS entry - JS fingerprint, JWT issuance | 1, 3, 7 |
| achel-xof.com / caish-djc.com / sumat-uah.com | Visitor registration / bot filter layer | 1, 3, 6, 7 |
| xml-v4.aasedformed-a.online | XML ad feed / click broker | 1 |
| click-for-preview.com (168.119.149.123) | Tracking & distribution hub | 1, 6, 7 |
| xml-v4.pushub.net (173.239.53.32) | Pushub push notification click endpoint | 2, 4, 5, 12 |
| beedirect.vip | Offer bidding & distribution hub | 2, 4, 5 |
| nachrichtenanalyse-online.click | Multi-campaign disinformation & fraud platform | 2, 4, 5 |
| shopli.city / dighlyconsive.com | Traffic broker / distribution hub | 3 |
| primechain-track.com (168.119.149.123) | Fake video player / VPN promotion | 6, 7 |
| press-to-see.com (168.119.149.123) | VPN affiliate entry (direct Play Store) | 10 |
| plenalo8.com | Casino affiliate rotator | 9 |
| pxl-us.rtb.tsyndicate.com | RTB ad exchange pixel | 12 |
| pornamigo.com | Push notification publisher network (lagerfeuer.net registered) | 12 |

The shared IP **168.119.149.123** across click-for-preview.com, primechain-track.com, and press-to-see.com establishes operational linkage between the general distribution hub (Chain 1) and the VPN promotion infrastructure (Chains 6, 7, 10) - indicating these are components of a single actor's toolkit.

---

## Disclaimer

All data in this report was collected through passive observation of publicly accessible network traffic. No systems were accessed without authorisation. Domain names, IP addresses, and redirect parameters are reproduced verbatim from observed network traffic for evidentiary purposes. This report is intended for use by security researchers, safe browsing teams, domain registrars, and regulatory authorities.

Observations are limited to the monitored time windows and traffic samples described above. Different redirect paths, offer rotations, or destination domains may exist outside these sessions. The absence of a specific domain or threat category from this report does not imply its absence from the infrastructure under investigation.

Screenshots for Chains 6–11 were captured in a desktop browser window during mobile traffic simulation. The redirect chains themselves were executed using a simulated Samsung Galaxy Fold 5 profile via Chrome DevTools. Final page rendering may therefore differ from what a native mobile browser would display.
