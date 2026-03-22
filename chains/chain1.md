# Chain 1 – Desktop Domain Redirection for lagerfeuer.net

**Tracked:** Thursday, 05 March 2026 · 20:00–21:00 CET · Desktop browser simulation
**Threat category:** Affiliate traffic fraud / Low-trust e-commerce

## Introduction

This chain documents the first recorded redirect sequence originating directly from lagerfeuer.net, ultimately landing at alishopmart.com - a low-trust e-commerce site. lagerfeuer.net operates as the TDS (Traffic Distribution System) entry point: it executes JavaScript-based bot detection and issues a signed JWT token before the server issues a 302 to achel-xof.com. That domain acts as the visitor-registration and fingerprinting layer: it registers the visit client-side via a meta redirect, then conditionally forwards qualifying traffic (non-bot, valid browser geometry) through xml-v4.aasedformed-a.online - an XML-based ad feed - and finally through click-for-preview.com, a tracking and distribution hub. The six-hop architecture is consistent with affiliate traffic laundering: each intermediate layer processes a commission click while obscuring the true origin from ad fraud detection systems.

## Redirect Flow

```
lagerfeuer.net (TDS entry - JS bot detection / JWT issuance)
→ achel-xof.com (visitor registration / bot filter)
→ xml-v4.aasedformed-a.online (XML ad feed / click broker)
→ click-for-preview.com (tracking & distribution hub)
→ alishopmart.com (final destination)
```

## Redirect Hops

| # | Status | IP | URL | Redirect Type | Notes |
|---|---|---|---|---|---|
| 1 | 200 | 212.92.104.5 | `http://lagerfeuer.net/` | javascript | Main domain |
| 2 | 302 | 212.92.104.5 | `https://lagerfeuer.net/?ch=1&js=eyJhbGciOiJIUz…` | temporary | - |
| 3 | 200 | 3.211.2.143 | `https://achel-xof.com/zclkvisitor/953261d6-18…` | meta | Analytics Provider / Bot Detection |
| 4 | 302 | 3.211.2.143 | `https://achel-xof.com/zclkredirect?visitid=95…` | temporary | - |
| 5 | 302 | 173.239.53.32 | `https://xml-v4.aasedformed-a.online/click?i=sKDpBr8H-iM_0` | temporary | - |
| 6 | 307 | 168.119.149.123 | `https://click-for-preview.com/index?cid=ddf9a3639a9e4…` | temporary | - |
| 7 | 200 | 2606:4700:3035::6815:975 | `https://alishopmart.com/?clickid=d6kqb16071bc73…` | none | - |

## Screenshots

![Maybe real Shopping Site](../pictures/lagerfeuer/chain-1/1.png)

## AI Security Analysis

*Automated threat assessment · claude-sonnet-4-6*

This chain is a textbook example of multi-layer affiliate traffic fraud. The six-hop architecture is deliberately designed to defeat attribution tools: each domain earns a commission click while the true origin - lagerfeuer.net - is buried under layers of redirectors.

From a user safety perspective, the final destination alishopmart.com is a low-trust e-commerce site with no verified identity. Users who arrive here and make purchases are at risk of payment card fraud, non-delivery of goods, and personal data harvesting. The JavaScript-based bot detection layer (achel-xof.com) specifically targets human users, ensuring that only real potential victims - not security scanners - reach the final destination.

The use of a signed JWT token for bot gating is particularly sophisticated: it ties each session to a cryptographically verified identity, preventing security researchers from replaying the chain. Internet users should treat any unsolicited browser redirect arriving via a push notification with extreme caution, especially when it lands on an unfamiliar shopping platform.

---
*Generated with Claude · lagerfeuer.net Domain Abuse Report · claude-sonnet-4-6*

## Raw Redirect Data

| Status Code | URL | IP | Page Type | Redirect Type | Redirect URL |
|---|---|---|---|---|---|
| 200 | `https://lagerfeuer.net/` | 212.92.104.5 | client_redirect | javascript | `https://lagerfeuer.net/?ch=1&js=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJKb2tlbiIsImV4cCI6MTc3MjczMjgzNCwiaWF0IjoxNzcyNzI1NjM0LCJpc3MiOiJKb2tlbiIsImpzIjoxLCJqdGkiOiIzMmN2cDRranR1bm5nN243dmcwdmtuMDIiLCJuYmYiOjE3NzI3MjU2MzQsInRzIjoxNzcyNzI1NjM0ODI0MzE3fQ.wASPrbmGI0xkRGf8BfYG7qS0zA4eZhikG6vj_IoYi-o&sid=af87bcf4-10ed-11f1-8b80-5093fc21bf10%27` |
| 302 | `https://lagerfeuer.net/?ch=1&js=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9…` | 212.92.104.5 | server_redirect | temporary | `http://achel-xof.com/zclkvisitor/953261d6-18aa-11f1-a54c-1237574ff1cd/72092e88-2c53-401c-b988-51ef43ce1034?campaignid=95480cb5-18aa-11f1-a54c-1237574ff1cd` |
| 200 | `https://achel-xof.com/zclkvisitor/953261d6-18aa-11f1-a54c-1237574ff1cd/72092e88-2c53-401c-b988-51ef43ce1034?campaignid=95480cb5-18aa-11f1-a54c-1237574ff1cd` | 3.211.2.143 | client_redirect | meta | `https://achel-xof.com/zclkvisitor/953261d6-18aa-11f1-a54c-1237574ff1cd/'https://achel-xof.com/zclkredirect?visitid=953261d6-18aa-11f1-a54c-1237574ff1cd&type=meta%27` |
| 302 | `https://achel-xof.com/zclkredirect?visitid=953261d6-18aa-11f1-a54c-1237574ff1cd&type=js&browserWidth=2007&browserHeight=962&iframeDetected=false&webdriverDetected=false&gpu=Google%20Inc.%20(AMD)…&timezone=UTC%2B01%3A00&timezoneName=Europe%2FBerlin` | 3.211.2.143 | server_redirect | temporary | `http://xml-v4.aasedformed-a.online/click?i=sKDpBr8H-iM_0` |
| 302 | `https://xml-v4.aasedformed-a.online/click?i=sKDpBr8H-iM_0` | 173.239.53.32 | server_redirect | temporary | `https://click-for-preview.com/index?cid=ddf9a3639a9e454eb7dbfc433b4fc4e2&extclickid=i3Qh7pLmeAU&bid=0.02&t1=14475043876&t2=8910802&type=default&referrer=lagerfeuer.net&campaign=2284886&keyword=*&source=211087.14475043876&pubfeed=211087` |
| 307 | `https://click-for-preview.com/index?cid=ddf9a3639a9e454eb7dbfc433b4fc4e2&extclickid=i3Qh7pLmeAU…` | 168.119.149.123 | server_redirect | temporary | `https://alishopmart.com/?clickid=d6kqb16071bc73fnr8h0` |
| 200 | `https://alishopmart.com/?clickid=d6kqb16071bc73fnr8h0` | 2606:4700:3035::6815:975 | normal | none | none |
