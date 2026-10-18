# TikTok Events API for Shopify — Free Server-Side Tracking

A complete, importable [Make.com](https://www.make.com/) blueprint that sends Shopify purchase events to the **TikTok Events API** server-side, so iOS privacy restrictions and ad blockers in the browser cannot stop the purchase event.

This is free and runs standalone. No app, no monthly fee.

📖 **Full setup guide with screenshots:** https://stackarchitect.xyz/tiktok-events-api-shopify/

---

## What it does

```
Shopify (Order payment webhook)  →  Make.com (Webhooks module)  →  HTTP POST  →  TikTok Events API
```

When a customer pays, Shopify fires an `orders/paid` webhook to Make.com. The scenario hashes the customer's data (SHA-256, per TikTok's spec), builds a `CompletePayment` event with Advanced Matching fields, and POSTs it to the TikTok Events API — entirely server-to-server, invisible to the browser.

**Result:** TikTok receives each paid order with hashed email and phone, IP and user agent, the data its Event Match Quality score is calculated from. We publish no typical score; read your own in Events Manager after a week of orders. It runs on Make.com's free tier.

---

## Files

| File | What it is |
|------|-----------|
| `blueprint.json` | The importable Make.com scenario. |
| `field-mapping.md` | Which Shopify order fields map to which TikTok parameters |

> **Fixed 18 Oct 2026.** Earlier versions of `blueprint.json` sent a fixed test event (`event_id` `test_123`, a fixed time and a $10 value) instead of each order's data, nested the customer fields under an Events 1.0 `context` object, and hashed the email without lower-casing it. If you imported it before this date, re-import it or replace the HTTP module's body with the one in `blueprint.json`.

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
4. **Credentials**: in the HTTP module, replace `YOUR_PIXEL_ID` and `YOUR_ACCESS_TOKEN` with your TikTok values. The body is raw JSON; check that the `{{...}}` expressions show as mapped items after import.
5. **Test**: place a test order. In TikTok Ads Manager → Assets → Events → your pixel → **Test Events**, confirm a server-side `CompletePayment` appears with the order's real value and currency, and that no duplicate purchase appears alongside the pixel's.

Detailed version, with troubleshooting: https://stackarchitect.xyz/tiktok-events-api-shopify/

---

## FAQ

**Does this replace my browser Pixel?**
No, run both. TikTok recommends Events API *alongside* the Pixel. TikTok merges the two only when they carry the same `event_id`; this blueprint uses the Shopify order ID, and Shopify's TikTok app does not document the ID its pixel sends, so check Test Events and Diagnostics for duplicates.

**Why `CompletePayment` and not `Purchase`?**
TikTok's purchase event is named `CompletePayment` (unlike Meta/Google's `Purchase`). Using the wrong name means events won't optimise campaigns.

**Can one scenario feed TikTok *and* Meta?**
Yes: add a Router module and branch to each platform's API. A pre-configured TikTok + Meta build is in the [Complete Kit](https://stackarchitect.xyz/pro/). For Google Ads, start with enhanced conversions in Shopify's Google & YouTube app; Shopify orders carry no Google click ID for a server upload to use.

**Is it really free?**
Make.com's free plan is 1,000 credits a month. How many orders that covers depends on the credits each run uses, shown in your scenario history. Past that, see [when to upgrade your free Make.com plan](https://stackarchitect.xyz/blog/when-to-upgrade-free-make-google-workspace/).

---

Maintained by [Stack Architect](https://stackarchitect.xyz/) · free Shopify automation guides & tools.
