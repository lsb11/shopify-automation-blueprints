# Free Shopify Automation Blueprints for Make.com

Open-source [Make.com](https://www.make.com/) scenario blueprints that add **server-side tracking and inventory automation to Shopify for $0/month** — no apps, no monthly SaaS fees, no code.

This repo gives you one complete, importable blueprint free: **TikTok Events API server-side tracking**. Import it, add two keys, and you're sending server-side `CompletePayment` events to TikTok in about six minutes — the same setup tools like WeltPixel and Analyzify charge $39–$299/month for.

Built and maintained by [Stack Architect](https://stackarchitect.xyz/) — free Shopify automation guides and tools.

---

## What's in here

| Scenario | What it does | Status |
|----------|-------------|--------|
| **[TikTok Events API](scenarios/tiktok-events-api/)** | Server-side `CompletePayment` events to TikTok, bypassing iOS & ad blockers. EMQ 6–8. | ✅ Free, full blueprint |
| CAPI Shield (Meta + Google) | Server-side Conversions API for Meta & Google Enhanced Conversions | 📦 In the [Complete Kit](https://stackarchitect.xyz/pro/) |
| Stocky Swap | Free inventory system to replace Shopify Stocky before its Aug 2026 shutdown | 📦 In the [Complete Kit](https://stackarchitect.xyz/pro/) |
| P&L Auto | Live profit & loss reporting in Google Sheets | 📦 In the [Complete Kit](https://stackarchitect.xyz/pro/) |

The TikTok blueprint here is the real thing, not a teaser — it runs standalone. The other three are bundled, pre-configured, with Google Sheets templates and setup support, in the [$29 Complete Kit](https://stackarchitect.xyz/pro/).

---

## Quick start — TikTok Events API in ~6 minutes

You'll need a free [Make.com](https://www.make.com/) account, a Shopify store, and a TikTok Ads Manager pixel.

1. **Sign up for Make.com free** — 1,000 operations/month, no card. Enough for stores up to ~300 orders/month.
2. **Import the blueprint** — download [`scenarios/tiktok-events-api/blueprint.json`](scenarios/tiktok-events-api/), then in Make.com: *Create a new scenario → ⋯ menu → Import Blueprint*.
3. **Copy your webhook URL** — open the Webhooks module in the imported scenario and copy the generated URL.
4. **Add the Shopify webhook** — Shopify Admin → Settings → Notifications → Webhooks → create one for **Order payment**, paste your Make.com URL, format JSON.
5. **Add your credentials** — in the HTTP module, replace `YOUR_PIXEL_ID` and `YOUR_ACCESS_TOKEN` with your values from TikTok Ads Manager.
6. **Test** — place a test order, then check TikTok Ads Manager → Events → Test Events for a server-side `CompletePayment` within 2–3 minutes.

Full walkthrough with screenshots: **[TikTok Events API for Shopify setup guide](https://stackarchitect.xyz/tiktok-events-api-shopify/)**.

---

## Why server-side tracking?

iOS privacy changes and ad blockers drop 20–40% of browser-pixel purchase events. Server-side tracking sends the purchase from your server (via Make.com) directly to the ad platform's API, so it's invisible to the browser-side blocking. You recover conversions your pixel is silently losing.

Background reading (all free):
- [Shopify server-side tracking: the complete setup guide](https://stackarchitect.xyz/blog/shopify-server-side-tracking-complete-setup-guide/)
- [Recover lost Shopify conversions with CAPI Shield](https://stackarchitect.xyz/capi-shield/)
- [How to fix Shopify conversion tracking after iOS updates](https://stackarchitect.xyz/blog/how-to-fix-shopify-conversion-tracking-after-ios-updates/)

---

## Who maintains this

[Stack Architect](https://stackarchitect.xyz/) builds free Shopify automation systems using Make.com and Google Sheets — replacing expensive apps with $0 automation. Free guides and tools at **[stackarchitect.xyz](https://stackarchitect.xyz/)**.

If these blueprints save you money, a ⭐ on the repo helps others find them.

## License

[MIT](LICENSE) — use, modify, and share freely.

## Contributing

Found a bug or improved a scenario? See [CONTRIBUTING.md](.github/CONTRIBUTING.md). Issues and PRs welcome.
