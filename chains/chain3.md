# Chain 3 – Desktop Domain Redirection for lagerfeuer.net

**Tracked:** Thursday, 05 March 2026 · 20:00–21:00 CET · Desktop browser simulation
**Threat category:** Affiliate traffic laundering

## Introduction

This is the longest desktop chain recorded, spanning eleven hops from lagerfeuer.net to climamarket.com - a Spanish-market air conditioner retailer. The sequence begins identically to Chain 1: lagerfeuer.net's TDS entry point issues a JavaScript bot detection challenge with JWT token issuance, then hands off to caish-djc.com for visitor registration and fingerprinting. What sets Chain 3 apart is the involvement of shopli.city, a traffic broker that redirects through dighlyconsive.com (a distribution hub) twice in a loop before resolving to the Kelkoo affiliate network. Kelkoo (de-go.kelkoogroup.net) is a legitimate price-comparison affiliate network - its presence here indicates that the upstream malvertising infrastructure is being used to route non-organic traffic into a legitimate affiliate attribution pipeline, potentially generating commissions without user intent.

## Redirect Flow

```
lagerfeuer.net (TDS entry - JS bot detection / JWT issuance)
→ caish-djc.com (visitor registration / bot filter)
→ shopli.city (traffic broker)
→ dighlyconsive.com (distribution hub)
→ shopli.city (traffic broker - second pass)
→ de-go.kelkoogroup.net (Kelkoo affiliate network)
→ climamarket.com (final destination)
```

## Redirect Hops

| # | Status | IP | URL | Redirect Type | Notes |
|---|---|---|---|---|---|
| 1 | 200 | 212.92.104.5 | `https://lagerfeuer.net/` | javascript | Main Domain |
| 2 | 302 | 212.92.104.5 | `https://lagerfeuer.net/?ch=1&js=eyJhbGciOiJIUz…` | temporary | Redirect Analytics Provider |
| 3 | 200 | 52.6.182.153 | `http://caish-djc.com/zclkvisitor/a521aab0-18…` | meta | Analytics Provider / Bot Detection |
| 4 | 302 | 52.6.182.153 | `http://caish-djc.com/zclkredirect?visitid=a5…` | temporary | - |
| 5 | 200 | 34.111.179.208 | `https://shopli.city/raini?rain=https%3A%2F%…` | javascript | Traffic Broker |
| 6 | 307 | 2600:9000:275f:cc00:16:c25e:32c0:93a1 | `https://dighlyconsive.com/8ca9a3b8-eb48-4286-940d…` | temporary | Distribution Hub |
| 7 | 302 | 2600:9000:275f:cc00:16:c25e:32c0:93a1 | `https://dighlyconsive.com/8ca9a3b8-eb48-4286-940d…` | temporary | - |
| 8 | 200 | 34.111.179.208 | `https://shopli.city/rainotest?rain=https://…` | javascript | Traffic Broker |
| 9 | 200 | 95.211.116.26 | `https://de-go.kelkoogroup.net/permanentLinkGo?country…` | javascript | Affiliate Network (Kelkoo) |
| 10 | 303 | 95.211.116.26 | `https://de-go.kelkoogroup.net/redirect?country=de&k=6…` | temporary | Affiliate Network (Kelkoo) |
| 11 | 302 | 2620:127:f00f:e:: | `https://climamarket.com/de/products/samsung-win…` | temporary | Locale Redirect |
| 12 | 200 | 2620:127:f00f:e:: | `https://climamarket.com/de-de/products/samsung-…` | none | Final Destination |

## Screenshots

![Maybe real Climamarket Shop Page](../pictures/lagerfeuer/chain-3/1.png)

## AI Security Analysis

*Automated threat assessment · claude-sonnet-4-6*

Chain 3 is the most technically complex chain in this dataset and demonstrates a form of affiliate traffic laundering that directly affects legitimate businesses. The Kelkoo affiliate network is a real, established price-comparison service used by thousands of European retailers. By routing non-organic traffic into Kelkoo's attribution pipeline, the operators of this chain potentially receive affiliate commissions for consumer visits that were not generated through legitimate user intent.

The impact on internet users is indirect but real: affiliate fraud inflates merchant customer acquisition costs, which are ultimately passed on to consumers through higher prices. The shopli.city → dighlyconsive.com double redirect is a deliberate obfuscation layer - each operator can claim they merely forwarded traffic from an apparently legitimate upstream source, creating plausible deniability throughout the chain.

The final destination (climamarket.com) is a genuine retailer. Users who arrive there are not in immediate danger - but their click has financially enriched a fraud network. This makes Chain 3 particularly insidious: it causes measurable financial harm to the broader e-commerce ecosystem without exposing individual users to obvious risk.

---
*Generated with Claude · lagerfeuer.net Domain Abuse Report · claude-sonnet-4-6*

## Raw Redirect Data

| Status Code | URL | IP | Page Type | Redirect Type | Redirect URL |
|---|---|---|---|---|---|
| 200 | `https://lagerfeuer.net/` | 212.92.104.5 | client_redirect | javascript | `https://lagerfeuer.net/?ch=1&js=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJKb2tlbiIsImV4cCI6MTc3MjczMjg2MSwiaWF0IjoxNzcyNzI1NjYxLCJpc3MiOiJKb2tlbiIsImpzIjoxLCJqdGkiOiIzMmN2cDY2Y3UwOTlxMHNhbDgwdjVhOGIiLCJuYmYiOjE3NzI3MjU2NjEsInRzIjoxNzcyNzI1NjYxNTUwNDY1fQ.jMiXoZU66vJXJojZVRgnxJohSZId3tNMhF8ldMiiXHo&sid=af87bcf4-10ed-11f1-8b80-5093fc21bf10%27` |
| 302 | `https://lagerfeuer.net/?ch=1&js=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9…` | 212.92.104.5 | server_redirect | temporary | `http://caish-djc.com/zclkvisitor/a521aab0-18aa-11f1-a54c-1237574ff1cd/72092e88-2c53-401c-b988-51ef43ce1034?campaignid=6500e1d0-7c06-11f0-809b-0affd781626d` |
| 200 | `http://caish-djc.com/zclkvisitor/a521aab0-18aa-11f1-a54c-1237574ff1cd/72092e88-2c53-401c-b988-51ef43ce1034?campaignid=6500e1d0-7c06-11f0-809b-0affd781626d` | 52.6.182.153 | client_redirect | meta | `http://caish-djc.com/zclkredirect?visitid=a521aab0-18aa-11f1-a54c-1237574ff1cd&type=meta` |
| 302 | `http://caish-djc.com/zclkredirect?visitid=a521aab0-18aa-11f1-a54c-1237574ff1cd&type=js&browserWidth=2007&browserHeight=962&iframeDetected=false&webdriverDetected=false&gpu=Google%20Inc.%20(AMD)…&timezone=UTC%2B01%3A00&timezoneName=Europe%2FBerlin` | 52.6.182.153 | server_redirect | temporary | `https://shopli.city/raini?rain=https%3A%2F%2Fdighlyconsive.com/8ca9a3b8-eb48-4286-940d-c015c0ed5818?hp=&geo=de&oadest=&traffic_type=01-Nipuhim&sub_id=uniform-kue-v244q2o9d9&brand=DE-offers-mehilaRON&adv_price=0.008500&click_id=zra521aab018aa11f1a54c1237574ff1cd58ef67814cd140529f4a8109ee7b56f909795965b42ffe8b1f` |
| 200 | `https://shopli.city/raini?rain=…` | 34.111.179.208 | client_redirect | javascript | `https://dighlyconsive.com/8ca9a3b8-eb48-4286-940d-c015c0ed5818?geo=de&oadest=&traffic_type=01-Nipuhim&sub_id=uniform-kue-v244q2o9d9&brand=DE-offers-mehilaRON&adv_price=0.008500&click_id=zra521aab018aa11f1a54c1237574ff1cd58ef67814cd140529f4a8109ee7b56f909795965b42ffe8b1f&ctrl_fetch_dest=document&ctrl_ab=ckud` |
| 307 | `https://dighlyconsive.com/8ca9a3b8-eb48-4286-940d-c015c0ed5818?…` | 2600:9000:275f:cc00:16:c25e:32c0:93a1 | server_redirect | temporary | `https://dighlyconsive.com/8ca9a3b8-eb48-4286-940d-c015c0ed5818/2?geo=de&oadest=&traffic_type=01-Nipuhim&sub_id=uniform-kue-v244q2o9d9&brand=DE-offers-mehilaRON&adv_price=0.008500&click_id=zra521aab018aa11f1a54c1237574ff1cd58ef67814cd140529f4a8109ee7b56f909795965b42ffe8b1f&ctrl_fetch_dest=document&ctrl_ab=ckud` |
| 302 | `https://dighlyconsive.com/8ca9a3b8-eb48-4286-940d-c015c0ed5818/2?…` | 2600:9000:275f:cc00:16:c25e:32c0:93a1 | server_redirect | temporary | `https://shopli.city/rainotest?rain=https://de-go.kelkoogroup.net/permanentLinkGo?country=de&id=47692679-139a-4232-9170-574f76601827&merchantUrl=https%3A%2F%2Fclimamarket.com%2Fde%2Fproducts%2Fsamsung-windfree-black-trial-split-air-conditioner-9000-9000-9000-btu-inverter-a-wifi-external-unit-5-2-kw&publisherSubId=shoplicity&ctrl_ab=ckud&publisherClickId=wuf3n3p6639bpnogjid38q6s` |
| 200 | `https://shopli.city/rainotest?rain=…` | 34.111.179.208 | client_redirect | javascript | `https://de-go.kelkoogroup.net/permanentLinkGo?country=de&id=47692679-139a-4232-9170-574f76601827&merchantUrl=https%3A%2F%2Fclimamarket.com%2Fde%2Fproducts%2Fsamsung-windfree-black-trial-split-air-conditioner-9000-9000-9000-btu-inverter-a-wifi-external-unit-5-2-kw&publisherSubId=shoplicity&publisherClickId=wuf3n3p6639bpnogjid38q6s` |
| 200 | `https://de-go.kelkoogroup.net/permanentLinkGo?…` | 95.211.116.26 | client_redirect | javascript | `https://de-go.kelkoogroup.net/redirect?country=de&k=612f7a9541cd6ea6c9a780de621954da2285ab75…` |
| 303 | `https://de-go.kelkoogroup.net/redirect?country=de&k=612f7a9541cd6ea6c9a780de…` | 95.211.116.26 | server_redirect | temporary | `https://climamarket.com/de/products/samsung-windfree-black-trial-split-air-conditioner-9000-9000-9000-btu-inverter-a-wifi-external-unit-5-2-kw?kk=a4c6294-19cbeaef7a5-13aa67&utm_source=kelkoode&utm_medium=cpc&utm_campaign=kelkooclick&utm_source_platform=KelkooGroup` |
| 302 | `https://climamarket.com/de/products/samsung-windfree-black-trial-split-air-conditioner-9000-9000-9000-btu-inverter-a-wifi-external-unit-5-2-kw?…` | 2620:127:f00f:e:: | server_redirect | temporary | `https://climamarket.com/de-de/products/samsung-windfree-black-trial-split-air-conditioner-9000-9000-9000-btu-inverter-a-wifi-external-unit-5-2-kw?kk=a4c6294-19cbeaef7a5-13aa67&utm_source=kelkoode&utm_medium=cpc&utm_campaign=kelkooclick&utm_source_platform=KelkooGroup` |
| 200 | `https://climamarket.com/de-de/products/samsung-windfree-black-trial-split-air-conditioner-9000-9000-9000-btu-inverter-a-wifi-external-unit-5-2-kw?…` | 2620:127:f00f:e:: | normal | none | none |
