# Service Codes (plain language)

What this is
- A short, plain-language explanation of the `service` codes used by the API for platform-specific virtual numbers and rentals.

When to use
- Include the `service` parameter in API calls when you want a number tailored for a specific platform (for example Instagram, WhatsApp, Telegram).

Common service codes (examples)
- `ig` — Instagram
- `wa` — WhatsApp
- `tg` — Telegram
- `fb` — Facebook

Basic usage example (buy a one-time virtual number)

```powershell
curl -X POST "https://api.proxnum.com/api/v1/resell/virtual/buy" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"service":"ig","country":6}'
```

Basic usage example (rent a number)

```powershell
curl -X POST "https://api.proxnum.com/api/v1/resell/rental/buy" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"service":"wa","country":6,"time":24}'
```

Notes
- Service codes are short identifiers accepted by all API endpoints that accept a `service` parameter.
- If you need a code not listed here, contact the API provider or check the original `services` view for the full mapping.
