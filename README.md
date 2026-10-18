# Free Shopify Automation Blueprints for Make.com

Open-source [Make.com](https://www.make.com/) scenario blueprints that add **server-side tracking to Shopify for $0/month** — no apps, no monthly SaaS fees, no code.

The flagship blueprint here is complete and standalone: **TikTok Events API server-side tracking**. Import it, add two keys and one Shopify webhook, and Shopify purchases reach TikTok's Events API from the server, without a monthly fee.

MIT-licensed. Fork it, modify it, ship it.

---

## What's in here

| Blueprint | What it does |
|-----------|--------------|
| **[TikTok Events API](scenarios/tiktok-events-api/)** | Server-side `CompletePayment` events to TikTok via Make.com, with hashed email and phone, IP and user agent for matching. |

This is a real, runnable blueprint — not a teaser or a lead magnet. Everything you need to deploy it is in this repo: the importable JSON, the field mapping, and the step-by-step setup below.

---

## Quick start: TikTok Events API

You'll need a free [Make.com](https://www.make.com/) account, a Shopify store, and a TikTok Ads Manager pixel.

1. **Sign up for Make.com (free)**: 1,000 credits a month, no card required. How many orders that covers depends on the credits each run uses, which your scenario history shows.
2. **Import the blueprint** — download [`scenarios/tiktok-events-api/blueprint.json`](scenarios/tiktok-events-api/), then in Make.com: *Create a new scenario → ⋯ menu → Import Blueprint*.
3. **Copy your webhook URL** — open the Webhooks module in the imported scenario and copy the generated URL.
4. **Add the Shopify webhook** — Shopify Admin → Settings → Notifications → Webhooks → create one for **Order payment**, paste your Make.com URL, format JSON.
5. **Add your credentials**: in the HTTP module, replace `YOUR_PIXEL_ID` and `YOUR_ACCESS_TOKEN` with your values from TikTok Ads Manager.
6. **Keep failed runs**: the blueprint turns on *Allow storing of incomplete executions*, so a rejected request is kept for retry instead of disappearing. Leave it on.
7. **Test**: place a test order, then check TikTok Ads Manager → Events → Test Events for a server-side `CompletePayment` with the order's real value and currency.

A full walkthrough with screenshots is available in the [TikTok Events API Shopify setup guide](https://stackarchitect.xyz/tiktok-events-api-shopify/).

---

## Why server-side tracking?

iOS privacy features, cookie limits and ad blockers stop some browser-pixel purchase events reaching ad platforms. How many depends on your traffic; there is no reliable average, which is why the [iOS attribution gap benchmark](https://stackarchitect.xyz/shopify-ios-attribution-gap-benchmark/) collects real store figures rather than quoting one. Server-side tracking sends the purchase from Make.com directly to the ad platform's API, so browser-side blocking cannot stop it.

The same Make.com pattern can be extended to Meta's Conversions API. Google Ads is different: Shopify orders carry no Google click ID, so for most stores the free fix there is enhanced conversions in Shopify's Google & YouTube app ([why](https://stackarchitect.xyz/shopify-google-ads-conversion-tracking/)).

Further reading (all free, no signup):
- [Shopify server-side tracking: the complete setup guide](https://stackarchitect.xyz/blog/shopify-server-side-tracking-complete-setup-guide/)
- [How to fix Shopify conversion tracking after iOS updates](https://stackarchitect.xyz/blog/how-to-fix-shopify-conversion-tracking-after-ios-updates/)

---

## What this blueprint does and doesn't do

**Does:** sends server-side `CompletePayment` events to TikTok on confirmed Shopify payment, with hashed email/phone for event matching. Runs on Make.com's free tier for typical small-store volume.

**Doesn't:** it doesn't replace your browser pixel; run both. TikTok merges a browser and a server event only when both carry the same `event_id`; this blueprint uses the Shopify order ID, and Shopify's TikTok app does not document the ID its pixel sends, so check Test Events and Diagnostics for duplicates. It won't backfill historical orders, and higher-volume stores may need a paid Make.com plan for the credits.

No tracking setup is fire-and-forget — verify your events in TikTok Events Manager after deploying and periodically after that.

---

## Maintained by

[Stack Architect](https://stackarchitect.xyz/) publishes free Shopify automation guides and tools built on Make.com and Google Sheets. Pre-configured versions of additional scenarios (Meta Conversions API, inventory, P&L) with Google Sheets templates are available separately as an optional [paid kit](https://stackarchitect.xyz/pro/) — but everything you need to run the TikTok blueprint is free and in this repo.

If it saves you money, a ⭐ helps others find it.

## Contributing

Found a bug or improved a scenario? Issues and PRs are welcome — see [CONTRIBUTING.md](.github/CONTRIBUTING.md).

## License

[MIT](LICENSE) — use, modify, and share freely.
