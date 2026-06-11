# Free Shopify Automation Blueprints for Make.com

Open-source [Make.com](https://www.make.com/) scenario blueprints that add **server-side tracking to Shopify for $0/month** — no apps, no monthly SaaS fees, no code.

The flagship blueprint here is complete and standalone: **TikTok Events API server-side tracking**. Import it, add two keys, and you're sending server-side `CompletePayment` events to TikTok in about six minutes — the same outcome tools like WeltPixel and Analyzify charge $39–$299/month for.

MIT-licensed. Fork it, modify it, ship it.

---

## What's in here

| Blueprint | What it does |
|-----------|--------------|
| **[TikTok Events API](scenarios/tiktok-events-api/)** | Server-side `CompletePayment` events to TikTok via Make.com, bypassing iOS restrictions and ad blockers. Typical EMQ 6–8. |

This is a real, runnable blueprint — not a teaser or a lead magnet. Everything you need to deploy it is in this repo: the importable JSON, the field mapping, and the step-by-step setup below.

---

## Quick start — TikTok Events API in ~6 minutes

You'll need a free [Make.com](https://www.make.com/) account, a Shopify store, and a TikTok Ads Manager pixel.

1. **Sign up for Make.com (free)** — 1,000 operations/month, no card required. Enough for stores up to ~300 orders/month.
2. **Import the blueprint** — download [`scenarios/tiktok-events-api/blueprint.json`](scenarios/tiktok-events-api/), then in Make.com: *Create a new scenario → ⋯ menu → Import Blueprint*.
3. **Copy your webhook URL** — open the Webhooks module in the imported scenario and copy the generated URL.
4. **Add the Shopify webhook** — Shopify Admin → Settings → Notifications → Webhooks → create one for **Order payment**, paste your Make.com URL, format JSON.
5. **Add your credentials** — in the HTTP module, replace `YOUR_PIXEL_ID` and `YOUR_ACCESS_TOKEN` with your values from TikTok Ads Manager.
6. **Test** — place a test order, then check TikTok Ads Manager → Events → Test Events for a server-side `CompletePayment` within 2–3 minutes.

A full walkthrough with screenshots is available [here](https://stackarchitect.xyz/tiktok-events-api-shopify/).

---

## Why server-side tracking?

iOS privacy changes and ad blockers drop an estimated 20–40% of browser-pixel purchase events. Server-side tracking sends the purchase from your server (via Make.com) directly to the ad platform's API, so it's invisible to browser-side blocking — you recover conversions your pixel is silently losing.

The same Make.com pattern in this blueprint can be extended to Meta's Conversions API and Google Enhanced Conversions; the TikTok scenario here is a clean, self-contained starting point you can adapt.

Further reading (all free, no signup):
- [Shopify server-side tracking: the complete setup guide](https://stackarchitect.xyz/blog/shopify-server-side-tracking-complete-setup-guide/)
- [How to fix Shopify conversion tracking after iOS updates](https://stackarchitect.xyz/blog/how-to-fix-shopify-conversion-tracking-after-ios-updates/)

---

## What this blueprint does and doesn't do

**Does:** sends server-side `CompletePayment` events to TikTok on confirmed Shopify payment, with hashed email/phone for event matching. Runs on Make.com's free tier for typical small-store volume.

**Doesn't:** it doesn't replace your browser pixel — run both, with a matching `event_id`, so TikTok deduplicates. It won't backfill historical orders, and very high-volume stores (500+ orders/month) may need a paid Make.com tier for the operation count.

No tracking setup is fire-and-forget — verify your events in TikTok Events Manager after deploying and periodically after that.

---

## Maintained by

[Stack Architect](https://stackarchitect.xyz/) publishes free Shopify automation guides and tools built on Make.com and Google Sheets. Pre-configured versions of additional scenarios (Meta/Google CAPI, inventory, P&L) with Google Sheets templates are available separately as an optional [paid kit](https://stackarchitect.xyz/pro/) — but everything you need to run the TikTok blueprint is free and in this repo.

If it saves you money, a ⭐ helps others find it.

## Contributing

Found a bug or improved a scenario? Issues and PRs are welcome — see [CONTRIBUTING.md](.github/CONTRIBUTING.md).

## License

[MIT](LICENSE) — use, modify, and share freely.
