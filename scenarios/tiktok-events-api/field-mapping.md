# Shopify → TikTok Events API field mapping

How the Shopify `orders/paid` webhook payload maps to TikTok Events API parameters in the HTTP module. All PII is SHA-256 hashed before sending, per TikTok's spec.

| TikTok parameter | Source (Shopify webhook) | Hashed? |
|------------------|--------------------------|---------|
| `event` | constant: `CompletePayment` | no |
| `event_time` | `created_at` (Unix) | no |
| `event_id` | `id` (for Pixel dedup) | no |
| `user.email` | `email` | SHA-256 |
| `user.phone` | `phone` / `billing_address.phone` | SHA-256 |
| `user.ip` | `client_details.browser_ip` | no (TikTok hashes server-side) |
| `user.user_agent` | `client_details.user_agent` | no |
| `properties.value` | `total_price` | no |
| `properties.currency` | `currency` | no |
| `properties.contents` | `line_items[]` → content_id, quantity, price | no |

> Set the HTTP body to **Key-value (Map mode)** in Make.com so the hashing expressions (`sha256(...)`) evaluate rather than being sent as literal text.

Full explanation: https://stackarchitect.xyz/tiktok-events-api-shopify/
