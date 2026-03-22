# Chain 7 – Mobile Simulated Domain Redirections for lagerfeuer.net

**Tracked:** Thursday, 05 March 2026 · 20:00–21:00 CET · Mobile simulated browser
**Threat category:** Social engineering / VPN install prompt

## Introduction

Chain 7 demonstrates that lagerfeuer.net's TDS routes traffic differently depending on the visitor's device type. A direct visit on mobile triggers the same JavaScript bot detection and JWT issuance as Chain 1, but the TDS routes the subsequent redirect to sumat-uah.com rather than achel-xof.com - a different visitor-registration provider - indicating device-aware campaign selection at the TDS level. From sumat-uah.com the path converges with Chain 6: click-for-preview.com issues a 307 to primechain-track.com's fake video player promoting VPN installation. This mobile-specific routing confirms that lagerfeuer.net actively differentiates traffic by device type, directing mobile visitors toward the VPN promotion campaign.

## Redirect Flow

```
lagerfeuer.net (TDS entry - JS bot detection / JWT issuance)
→ sumat-uah.com (visitor registration / click redirector)
→ click-for-preview.com (tracking & distribution hub)
→ primechain-track.com (fake video player / VPN promotion)
```

## Redirect Hops

| # | Status | IP | URL | Redirect Type | Notes |
|---|---|---|---|---|---|
| 1 | 200 | 172.241.213.99 | `https://lagerfeuer.net/` | javascript | Main Domain – JS Bot Detection / JWT Issuance |
| 2 | 302 | 172.241.213.99 | `https://lagerfeuer.net/?ch=1&js=eyJhbGciOiJIUz…` | temporary | JWT Verification Redirect |
| 3 | 200 | 34.192.204.134 | `http://sumat-uah.com/zclkvisitor/66123a12-18…` | none | Visitor Registration |
| 4 | 302 | 34.192.204.134 | `http://sumat-uah.com/zclkredirect?visitid=66…` | temporary | Click Redirector |
| 5 | 307 | 168.119.149.123 | `https://click-for-preview.com/index?cid=0c2805273d7d4…` | temporary | Tracking & Distribution Hub → primechain-track.com |

## Screenshots

![This Site is already blocked](../pictures/lagerfeuer/chain-7/1.png)

## AI Security Analysis

*Automated threat assessment · claude-sonnet-4-6*

Chain 7 confirms that lagerfeuer.net actively routes traffic differently depending on the visitor's device type. Desktop visitors (Chains 1 and 3) are directed to e-commerce fraud and affiliate schemes; mobile visitors are routed to the VPN social engineering campaign via primechain-track.com. This device-aware targeting is a hallmark of sophisticated malvertising operations that have profiled their audience and tailored the attack vector accordingly.

The security implication for mobile users is significant: visiting lagerfeuer.net on a smartphone - even without interacting with any on-page content - initiates an automatic redirect chain terminating at a social engineering page. The JWT bot detection layer ensures this affects real human users with real browsers, specifically filtering out the automated scanners that would otherwise detect and report the abuse.

Given that the majority of German internet users primarily access the web via smartphone, this mobile-targeting strategy maximises the campaign's reach while minimising the likelihood of detection. Users should avoid visiting lagerfeuer.net on any device and should revoke any push notification permissions previously granted to the domain.

---
*Generated with Claude · lagerfeuer.net Domain Abuse Report · claude-sonnet-4-6*

## Raw Redirect Data

| Status Code | URL | IP | Page Type | Redirect Type | Redirect URL |
|---|---|---|---|---|---|
| 200 | `https://lagerfeuer.net/` | 172.241.213.99 | client_redirect | javascript | `https://lagerfeuer.net/?ch=1&js=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJKb2tlbiIsImV4cCI6MTc3MjczNDkwMywiaWF0IjoxNzcyNzI3NzAzLCJpc3MiOiJKb2tlbiIsImpzIjoxLCJqdGkiOiIzMmN2c3QwdmhkNHZrajlsZWMxNjZmY2UiLCJuYmYiOjE3NzI3Mjc3MDMsInRzIjoxNzcyNzI3NzAzMDQ1Nzk0fQ.hdj57saOnKkK5wWQhj-dnuqFULPPWel8MtmHgjt4r-c&sid=af87bcf4-10ed-11f1-8b80-5093fc21bf10%27` |
| 302 | `https://lagerfeuer.net/?ch=1&js=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9…` | 172.241.213.99 | server_redirect | temporary | `http://sumat-uah.com/zclkvisitor/66123a12-18af-11f1-a54c-1237574ff1cd/72092e88-2c53-401c-b988-51ef43ce1034?campaignid=0e71f710-e00a-11f0-bad9-0affd781626d` |
| 200 | `http://sumat-uah.com/zclkvisitor/66123a12-18af-11f1-a54c-1237574ff1cd/72092e88-2c53-401c-b988-51ef43ce1034?campaignid=0e71f710-e00a-11f0-bad9-0affd781626d` | 34.192.204.134 | normal | none | none |
| 302 | `http://sumat-uah.com/zclkredirect?visitid=66123a12-18af-11f1-a54c-1237574ff1cd&type=js&browserWidth=981&browserHeight=1178&iframeDetected=false&webdriverDetected=false&gpu=Google%20Inc.%20(AMD)…&timezone=UTC%2B01%3A00&timezoneName=Europe%2FBerlin` | 34.192.204.134 | server_redirect | temporary | `https://click-for-preview.com/index?cid=0c2805273d7d46b084f137290a75941e&extclickid=zr66123a1218af11f1a54c1237574ff1cdfc650aec744449998029f103515d5ce00979609e4936ea2ea1&cost=0.015000&t1=uniform-kue-v244q2o9d9&t2=0&type=default&keyword=lagerfeuer%2Clagerfeuer.net&source=badious-buzzard&campaign_id=2715915&keyword_match=broad&match=` |
| 307 | `https://click-for-preview.com/index?cid=0c2805273d7d46b084f137290a75941e&extclickid=zr66123a1218af11f1a54c1237574ff1cdfc650aec744449998029f103515d5ce00979609e4936ea2ea1…` | 168.119.149.123 | server_redirect | temporary | `https://primechain-track.com/video-player-2-1/?domain=click-for-preview.com&x=Tm9ybiBWUE4gYXBwbGljYXRpb24=` |
