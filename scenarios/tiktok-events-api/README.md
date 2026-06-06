# TikTok Events API for Shopify — Free Server-Side Tracking

A complete, importable [Make.com](https://www.make.com/) blueprint that sends Shopify purchase events to the **TikTok Events API** server-side — recovering the 20–40% of `CompletePayment` events lost to iOS privacy restrictions and ad blockers.

This is free and runs standalone. No app, no monthly fee.

📖 **Full setup guide with screenshots:** https://stackarchitect.xyz/tiktok-events-api-shopify/

---

## What it does

```
Shopify (Order payment webhook)  →  Make.com (Webhooks module)  →  HTTP POST  →  TikTok Events API
```

When a customer pays, Shopify fires an `orders/paid` webhook to Make.com. The scenario hashes the customer's data (SHA-256, per TikTok's spec), builds a `CompletePayment` event with Advanced Matching fields, and POSTs it to the TikTok Events API — entirely server-to-server, invisible to the browser.

**Result:** EMQ (Event Match Quality) scores of 6–8 in most stores, the same outcome WeltPixel ($39–$99/mo) and Analyzify ($99–$299/mo) deliver — at $0 on Make.com's free tier.

---

## Files

| File | What it is |
|------|-----------|
| `blueprint.json` | The importable Make.com scenario. *(Add your exported blueprint here — see note below.)* |
| `field-mapping.md` | Which Shopify order fields map to which TikTok parameters |

> **Maintainer note:** Export the working scenario from Make.com (scenario → ⋯ → *Export Blueprint*) and commit it as `blueprint.json`. Strip any real Pixel ID / Access Token first — the placeholders `YOUR_PIXEL_ID` and `YOUR_ACCESS_TOKEN` should remain so importers add their own.

---

## Setup

### Prerequisites
- Free [Make.com](https://www.make.com/) account
- Shopify store (any plan)
- TikTok Ads Manager pixel + Events API access token

### Steps

1. **Import** `blueprint.json` into Make.com (*New scenario → ⋯ → Import Blueprint*).
2. **Webhook URL** — open the Webhooks module, copy the generated URL.
3. **Shopify webhook** — Admin → Settings → Notifications → Webhooks → new webhook, event **Order payment**, paste the Make.com URL, format **JSON**, save.
4. **Credentials** — in the HTTP module, replace `YOUR_PIXEL_ID` and `YOUR_ACCESS_TOKEN` with your TikTok values. Set the HTTP body input to **Key-value (Map mode)** so Make.com expressions evaluate.
5. **Test** — place a test order. In TikTok Ads Manager → Assets → Events → your pixel → **Test Events**, confirm a server-side `CompletePayment` appears in 2–3 minutes. Aim for EMQ ≥ 6.

Detailed version, with troubleshooting: https://stackarchitect.xyz/tiktok-events-api-shopify/

---

## FAQ

**Does this replace my browser Pixel?**
No — run both. TikTok recommends Events API *alongside* the Pixel. Set a matching `event_id` so TikTok deduplicates and you don't double-count.

**Why `CompletePayment` and not `Purchase`?**
TikTok's purchase event is named `CompletePayment` (unlike Meta/Google's `Purchase`). Using the wrong name means events won't optimise campaigns.

**Can one scenario feed TikTok *and* Meta *and* Google?**
Yes — add a Router module and branch to each platform's API. That multi-platform build (CAPI Shield) is in the [Complete Kit](https://stackarchitect.xyz/pro/), pre-configured.

**Is it really free?**
Make.com's free tier is 1,000 ops/month — roughly 300 orders. Past that, see [when to upgrade your free Make.com plan](https://stackarchitect.xyz/blog/when-to-upgrade-free-make-google-workspace/).

---

Maintained by [Stack Architect](https://stackarchitect.xyz/) · free Shopify automation guides & tools.
