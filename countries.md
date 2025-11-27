# Country Codes (plain language)

What this is
- A short explanation of the numeric country codes used by the API. Use the numeric `country` value in requests when you need numbers from a specific country.

Example usage (get price / buy number)

```powershell
curl -X GET "https://api.proxnum.com/api/v1/resell/price?service=ig&country=6" \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -H "Accept: application/json"

curl -X POST "https://api.proxnum.com/api/v1/resell/virtual/buy" \
  -H "Authorization: Bearer YOUR_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"service":"ig","country":6}'
```

Notes
- These numeric codes are the authoritative values used by the API (the site maps them to country names).
- If you do not know the numeric code for a country, use the site UI or the original `countries` Blade view for the complete mapping.

Tips
- Always check availability with the `price` or `rental/availability` endpoint before attempting to purchase.
