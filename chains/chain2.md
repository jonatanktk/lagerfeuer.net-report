# Chain 2 – Desktop Domain Redirection for lagerfeuer.net

**Tracked:** Thursday, 05 March 2026 · 20:00–21:00 CET · Desktop browser simulation
**Threat category:** Political disinformation (Merz/Chrupalla)

## Introduction

This chain enters via xml-v4.pushub.net - a Pushub push notification ad network click endpoint - and terminates at nachrichtenanalyse-online.click, a German-language political disinformation landing page promoting the Merz/Chrupalla narrative. Unlike Chain 1 which originates directly on lagerfeuer.net, this sequence begins at the push notification ad network layer, indicating lagerfeuer.net is registered as a Pushub publisher feeding traffic into the network's offer rotation. The intermediate domain beedirect.vip acts as a bidding and distribution hub, selecting the final destination based on offer parameters (campaign ID, pubfeed, bid amount) before issuing the terminal redirect. The three-hop structure is notably compact compared to the desktop chains, as Pushub-sourced traffic bypasses the bot detection layer.

## Redirect Flow

```
xml-v4.pushub.net (Pushub push notification click endpoint)
→ beedirect.vip (offer bidding & distribution hub)
→ nachrichtenanalyse-online.click (disinformation landing page)
```

## Redirect Hops

| # | Status | IP | URL | Redirect Type | Notes |
|---|---|---|---|---|---|
| 1 | 302 | 173.239.53.32 | `https://xml-v4.pushub.net/click2?i=RYwDYfX0oj4_0&…` | temporary | - |
| 2 | 302 | 2600:9000:2017:7c00:15:545f:c980:93a1 | `https://beedirect.vip/db4e0d00-f99b-4f6c-9c89…` | temporary | - |
| 3 | 200 | 2606:4700:3031::ac43:a5f8 | `https://nachrichtenanalyse-online.click/c/de/52_merzchrupalla/?…` | none | - |

## Screenshots

![Fake Tagesschau Page](../pictures/lagerfeuer/chain-2/1.png)

![All links go to this Formular](../pictures/lagerfeuer/chain-2/2.png)

## AI Security Analysis

*Automated threat assessment · claude-sonnet-4-6*

This chain delivers political content to German-speaking internet users via a push notification channel that subscribers likely associated with lagerfeuer.net. The landing page promotes a narrative around two prominent German politicians - a content pattern consistent with those classified as systemic disinformation risk under EU Digital Services Act Article 34.

The danger for internet users is subtle but severe: push notifications bypass most ad blockers and arrive with the visual authority of system-level alerts. Users clicking what they expect to be campfire or community content are instead served manufactured political material designed to alter their political beliefs. The use of a .click TLD for the final domain is a common pattern for disposable disinformation infrastructure - cheap, quickly replaced when flagged, and visually similar to legitimate news sources.

This chain constitutes a clear violation of multiple EU regulations, including the Digital Services Act (Article 34 - systemic risk from disinformation via advertising) and the ePrivacy Directive (unsolicited commercial communications without consent).

---
*Generated with Claude · lagerfeuer.net Domain Abuse Report · claude-sonnet-4-6*

## Raw Redirect Data

| Status Code | URL | IP | Page Type | Redirect Type | Redirect URL |
|---|---|---|---|---|---|
| 302 | `https://xml-v4.pushub.net/click2?i=RYwDYfX0oj4_0&ci=-6012402443632827597&j=rv%3Db%26ss%3D2048x1152…` | 173.239.53.32 | server_redirect | temporary | `https://beedirect.vip/db4e0d00-f99b-4f6c-9c89-aa5aa5ccb614?pubfeed_subid=965920_lagerfeuer.net&offer=3865151&banner=9477943&campaign=2309667&pubfeed=965920&subid=lagerfeuer.net&bid=0.015&clickid=rI*n1SSTIzM` |
| 302 | `https://beedirect.vip/db4e0d00-f99b-4f6c-9c89-aa5aa5ccb614?pubfeed_subid=965920_lagerfeuer.net&offer=3865151&banner=9477943&campaign=2309667&pubfeed=965920&subid=lagerfeuer.net&bid=0.015&clickid=rI*n1SSTIzM` | 2600:9000:2017:7c00:15:545f:c980:93a1 | server_redirect | temporary | `https://nachrichtenanalyse-online.click/c/de/52_merzchrupalla/?method=pop&regform=1&on=Norentia&icid=weosu609ul811nogjofo5t3m&traff=ee903878-3dd9-4e7f-a44a-09a84f313c34&cmp=db4e0d00-f99b-4f6c-9c89-aa5aa5ccb614` |
| 200 | `https://nachrichtenanalyse-online.click/c/de/52_merzchrupalla/?method=pop&regform=1&on=Norentia&icid=weosu609ul811nogjofo5t3m&traff=ee903878-3dd9-4e7f-a44a-09a84f313c34&cmp=db4e0d00-f99b-4f6c-9c89-aa5aa5ccb614` | 2606:4700:3031::ac43:a5f8 | normal | none | none |
