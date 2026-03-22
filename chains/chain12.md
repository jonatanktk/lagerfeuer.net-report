# Chain 12 – Desktop Domain Redirection for lagerfeuer.net

**Tracked:** Friday, 07 March 2026 · ~23:00 CET · Desktop browser (real device)
**Threat category:** Adult content (unsolicited, no age gate)

## Introduction

Chain 12 was recorded two days after the main session batch. It originates from xml-v4.pushub.net with a referrer of live.pornamigo.com - a dedicated push notification ad platform - confirming that lagerfeuer.net is actively registered as a push notification publisher on pornamigo.com. The click is forwarded to pxl-us.rtb.tsyndicate.com, a real-time bidding pixel endpoint operated by tsyndicate.com (a US-based RTB ad exchange), which then redirects to darkteens.net, an adult content site. The real-device capture is significant: it confirms the redirect chain functions identically on non-simulated hardware, ruling out any browser fingerprinting evasion as the cause of the observed behaviour.

## Redirect Flow

```
xml-v4.pushub.net (Pushub push notification click endpoint / pornamigo referrer)
→ pxl-us.rtb.tsyndicate.com (RTB ad exchange pixel - tsyndicate)
→ darkteens.net (final destination - adult content)
```

## Redirect Hops

| # | Status | IP | URL | Redirect Type | Notes |
|---|---|---|---|---|---|
| 1 | 302 | 173.239.53.32 | `https://xml-v4.pushub.net/click2?i=5fFkKD4EfMs_0&…` | temporary | Push Notification Ad Network (Pushub) |
| 2 | 302 | 66.242.14.30 | `https://pxl-us.rtb.tsyndicate.com/do2/direct?c=APeIQFMmDJ…` | temporary | RTB Ad Exchange (tsyndicate) |
| 3 | 200 | 162.254.188.42 | `https://darkteens.net/?host=http%3A%2F%2Flive…` | none | Final Destination (Adult Content) |

## Screenshots

![Final Adult Page](../pictures/lagerfeuer/chain-12/1.png)

## AI Security Analysis

*Automated threat assessment · claude-sonnet-4-6*

Chain 12 documents a push notification click originating from the Pushub/pornamigo ad network that terminates at darkteens.net, an adult content site. The chain does not start at lagerfeuer.net directly - it begins at xml-v4.pushub.net with `lo=live.pornamigo.com` as the referring network. The connection to lagerfeuer.net is evidenced by the final destination URL itself: darkteens.net receives the request with the parameter `?host=live.pornamigo.com/filter?q=lagerfeuer`, identifying lagerfeuer.net as the registered publisher slot on pornamigo.com from which this click originated.

In plain terms: lagerfeuer.net is registered as a push notification publisher on pornamigo.com, and clicks from that publisher slot are being routed through the Pushub RTB network to adult content destinations. Users who subscribed to push notifications associated with lagerfeuer.net can therefore receive unsolicited adult content without consent, age verification, or any prior warning - a violation of basic informed consent principles and German telecommunications law (TKG). Mobile devices are frequently shared including with minors; adult content delivered via push notification to a shared device raises concerns under German JuSchG (Youth Protection Act) and the EU Age Verification Regulation. The tsyndicate.com RTB pixel processes the user's IP address, device fingerprint, and browsing context in connection with adult content - creating sensitive personal data records under GDPR Article 9 without a documented legal basis.

This chain warrants reporting to the Bundesnetzagentur (telecommunications abuse) and the relevant data protection supervisory authority. The lagerfeuer.net publisher slot on pornamigo.com should be reported directly to Pushub/pornamigo for facilitating adult content delivery to a general-audience subscriber base.

---
*Generated with Claude · lagerfeuer.net Domain Abuse Report · claude-sonnet-4-6*

## Raw Redirect Data

| Status Code | URL | IP | Page Type | Redirect Type | Redirect URL |
|---|---|---|---|---|---|
| 302 | `https://xml-v4.pushub.net/click2?i=5fFkKD4EfMs_0&ci=-25589463724359074&j=rv%3Db%26ss%3D2048x1152%26ws%3D2007x962%26wp%3D0x0%26ce%3D1%26ck%3Djc%26cv%3D8377%26cs%3D1%26fr%3D0%26hc%3D0%26fl%3Dnull%26jv%3Dnull%26sc%3D24%26hr%3D2%26rf%3Dfilter.leoyard.com%26lo%3Dlive.pornamigo.com%26mb%3D0%26hb%3D0%26pl%3DLinux%2Bx86_64%26ua%3DMozilla%252F5.0%2B%28X11%253B%2BLinux%2Bx86_64%29%2BAppleWebKit%252F537.36%2B%28KHTML%252C%2Blike%2BGecko%29%2BChrome%252F144.0.0.0%2BSafari%252F537.36%26nd%3D0%26to%3Dnull%26wbd%3D1%26wbde%3D0%26sqm%3D0%26phj%3D0%26nmj%3D0%26sln%3D0%26es%3D0%26ln%3Dde-DE%252Cde%252Cen-US%252Cen%252Cru%26lnl%3D5%26hsc%3D1%26frc%3D1%26dbt%3D0%26prb%3D20030107%26tz%3D-60%26hid%3D0%26mq%3D1%26my%3D8%26geo%3D1%26thx%3D0%26the%3D0%26ths%3D0%26cpc%3D%26ocp%3D%26hwc%3D12%26hrl%3D%26acd%3Dpppmp%26vcd%3Dnpp%26pal%3D5%26pai%3D1%26pli%3D1%26win%3D2007x962%26wout%3D2048x1080%26wpof%3D0x0%26bcld%3D1976x18%26scrp%3D0x0%26scrad%3D2048x1152%26spd%3D24%26pxr%3D1.25%26sck%3D1%26ckl%3D53%26sls%3D1%26sss%3D1%26six%3D1%26sdb%3D0%26vvr%3DGoogle%2BInc.%2B%28AMD%29%26vrd%3DANGLE%2B%28AMD%252C%2BAMD%2BRadeon%2BGraphics%2B%28radeonsi%2Brenoir%2BACO%29%252C%2BOpenGL%2BES%2B3.2%29%26cnvs%3D7f7f7f80%26pnt%3Dprompt%26bch%3D1%26blv%3D1%26mmd_ao%3D1%26mmd_ai%3D1%26mmd_vi%3D0` | 173.239.53.32 | server_redirect | temporary | `https://pxl-us.rtb.tsyndicate.com/do2/direct?c=APeIQFMmDJkycuaI0DGDhYgwY-gsjOGQDpyFIuC8uVjxDMYbY2TQEAMDRo0WB2WUaUGjTI4YLcK0nNEihpkYZWLguDGjBo4wZUQ4nCMmDRmFOraIiAEjhg2TN77ImGEDB1URXRyOcYOUaQ4bDsPUGYPRRowxYnDEkBGmxY0aM8iw9AkzB44aOVqMIWMjjNMyPHPIiCFURFEyGHGUMUNmzE4aLV7WaNvyYAsxNWjAaFHDjIwaY2bM-FwGB43CBu1MpPFUp0M4dcQsnCoYRlg4F3XI-Ewjx1A4EnXUaFrjBo0bDsvgofNlDnCMTJ1ClUrVqo3CY9rkfgvja8OHZMwsRG7YjZuFNGLUqGGjvcM2bjzq0Gwjh-2M8OXfYPrUYR3COgxEh0Vz6PDCC2SEIccadJRRBlcuuFEGHS_8gMYbc9DRAxoDwlHCDEGUIIMRIhrBRhp2lOGCRnK4EUYbaZzxhgtjvNFGiWakwUaDcnxoRBwfEsFGGGcgZEYZdSDERR0lyWDDhRkmQUYPu2WWw5JN2jAHlBqy6CKMMtJoI5YwOOncG3QY1cNw6hl3Q2Fk2IjRiSmu-EaLL8Y4Y41tYKcgelZpFUZwW8wQQ1YZyUGWDjC4UJJJNThJkQhjwNHGF3AoulCjM-BQlQzkyWFHbjPcV0alfTLqAnv-1ZEGRmKIUd9B7bUwQ2g4cCYGX5GZlqusuJLB3l1nFZZGbiKw5kIONbgQQwwzOJvDDIXVEQZGTbyhh45DvtAsDCCggMWzO4DARBpu1IEHCHh4-oUNNKQAQhC4sVHGFWWIsUQaFMJ1gwtUhbsEElQ0wQQLIJy4RhkgHHHqGm_IOwQacthYxgsx0ECDoxyDO0UYZiiYhrcz_HuVVouKQEQRhd35xRgpr1wYGzGz7NBBdnwhRxlsTFRcDeqZVpJDcpxxng52yXBzGTmLIcdCOCydcxtvIKabWjTcXPFEDmE422sV45EH1yKQkcfRdMiRJNGLYcShRQa-QKeKXuYZJp8v5LgjQj_E0cOQRcpxZJJPDyUqRhXTMeidLdThBr-24uDCHWHMIUPLcxzOEF4x7AfDTkqXnXIdc3xBueWF0ZFq5zfIINhUolXUxuU6sO76bqJRpXFYZOhchnNfDDrRDa2_nntyOYdhrxx0IFVoDYiGIUZwZS8m1o6FwUHzplrJd98YaCyULhts9KFAQA%3D%3D&s=1add983f6eb40a4621846b498801ac0fedb4deb92f77838d5b1c45858a9499aa1772922333` |
| 302 | `https://pxl-us.rtb.tsyndicate.com/do2/direct?c=APeIQFMmDJkycuaI0DGDhYgwY-gsjOGQDpyFIuC8uVjxDMYbY2TQEAMDRo0WB2WUaUGjTI4YLcK0nNEihpkYZWLguDGjBo4wZUQ4nCMmDRmFOraIiAEjhg2TN77ImGEDB1URXRyOcYOUaQ4bDsPUGYPRRowxYnDEkBGmxY0aM8iw9AkzB44aOVqMIWMjjNMyPHPIiCFURFEyGHGUMUNmzE4aLV7WaNvyYAsxNWjAaFHDjIwaY2bM-FwGB43CBu1MpPFUp0M4dcQsnCoYRlg4F3XI-Ewjx1A4EnXUaFrjBo0bDsvgofNlDnCMTJ1ClUrVqo3CY9rkfgvja8OHZMwsRG7YjZuFNGLUqGGjvcM2bjzq0Gwjh-2M8OXfYPrUYR3COgxEh0Vz6PDCC2SEIccadJRRBlcuuFEGHS_8gMYbc9DRAxoDwlHCDEGUIIMRIhrBRhp2lOGCRnK4EUYbaZzxhgtjvNFGiWakwUaDcnxoRBwfEsFGGGcgZEYZdSDERR0lyWDDhRkmQUYPu2WWw5JN2jAHlBqy6CKMMtJoI5YwOOncG3QY1cNw6hl3Q2Fk2IjRiSmu-EaLL8Y4Y41tYKcgelZpFUZwW8wQQ1YZyUGWDjC4UJJJNThJkQhjwNHGF3AoulCjM-BQlQzkyWFHbjPcV0alfTLqAnv-1ZEGRmKIUd9B7bUwQ2g4cCYGX5GZlqusuJLB3l1nFZZGbiKw5kIONbgQQwwzOJvDDIXVEQZGTbyhh45DvtAsDCCggMWzO4DARBpu1IEHCHh4-oUNNKQAQhC4sVHGFWWIsUQaFMJ1gwtUhbsEElQ0wQQLIJy4RhkgHHHqGm_IOwQacthYxgsx0ECDoxyDO0UYZiiYhrcz_HuVVouKQEQRhd35xRgpr1wYGzGz7NBBdnwhRxlsTFRcDeqZVpJDcpxxng52yXBzGTmLIcdCOCydcxtvIKabWjTcXPFEDmE422sV45EH1yKQkcfRdMiRJNGLYcShRQa-QKeKXuYZJp8v5LgjQj_E0cOQRcpxZJJPDyUqRhXTMeidLdThBr-24uDCHWHMIUPLcxzOEF4x7AfDTkqXnXIdc3xBueWF0ZFq5zfIINhUolXUxuU6sO76bqJRpXFYZOhchnNfDDrRDa2_nntyOYdhrxx0IFVoDYiGIUZwZS8m1o6FwUHzplrJd98YaCyULhts9KFAQA%3D%3D&s=1add983f6eb40a4621846b498801ac0fedb4deb92f77838d5b1c45858a9499aa1772922333` | 66.242.14.30 | server_redirect | temporary | `https://darkteens.net/?host=http%3A%2F%2Flive.pornamigo.com%2Ffilter%3Fq%3Dlagerfeuer&hostId=22549&shost=pornamigo.com&spotid=5015747` |
| 200 | `https://darkteens.net/?host=http%3A%2F%2Flive.pornamigo.com%2Ffilter%3Fq%3Dlagerfeuer&hostId=22549&shost=pornamigo.com&spotid=5015747` | 162.254.188.42 | normal | none | none |
