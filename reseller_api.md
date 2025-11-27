# Reseller API — Short Reference (plain language)

Overview
- This is a concise summary of the reseller API endpoints you will call to get prices, buy virtual numbers, rent numbers, and check status. All responses are JSON. Use a Bearer token in the `Authorization` header.

Authentication
- Header: `Authorization: Bearer YOUR_API_TOKEN`
- Also include `Accept: application/json` and `Content-Type: application/json` for POST requests.

Common response (error format)

```json
{
  "success": false,
  "code": "no_numbers",
  "message": "No numbers available for the selected service and country"
}
```

Key endpoints (short)

- `GET /api/v1/resell/price?service=...&country=...`
  - Get base and sell price for a given service and country.

  Example:

  ```powershell
  curl -s -X GET "https://api.proxnum.com/api/v1/resell/price?service=ig&country=6" \
    -H "Authorization: Bearer YOUR_TOKEN" \
    -H "Accept: application/json"
  ```

- `POST /api/v1/resell/virtual/buy`
  - Buy a one-time virtual number. Body example: `{"service":"ig","country":6}`.

  Example:

  ```powershell
  curl -s -X POST "https://api.proxnum.com/api/v1/resell/virtual/buy" \
    -H "Authorization: Bearer YOUR_TOKEN" \
    -H "Content-Type: application/json" \
    -d '{"service":"ig","country":6}'
  ```

  Success response contains an `activation` object with `activation_id`, `phone`, and `status`.

- `GET /api/v1/resell/virtual/{id}/status`
  - Check status of an activation. `{id}` is the activation id or local DB id. Success when a code arrives will include `code`.

- `POST /api/v1/resell/virtual/resend`
  - Request a resend. Body: `{"activation_id":"..."}`.

- `POST /api/v1/resell/virtual/cancel`
  - Request cancellation and possible refund. Body: `{"activation_id":"..."}`.

- `GET /api/v1/resell/activations`
  - List activations for your account (paginated).

- Rental endpoints:
  - `POST /api/v1/resell/rental/buy` — buy a rental (`time` in hours)
  - `GET /api/v1/rental/availability?service=...&country=...&time=...` — check rental availability/price
  - `POST /api/v1/resell/rental/cancel` — cancel rental
  - `POST /api/v1/rental/{id}/extend` — extend rental time
  - `GET /api/v1/rentals/{rental_id}/messages` — fetch messages for a rental

Errors you may see
- `no_numbers` — no numbers available for the service/country
- `insufficient_balance` — not enough credit
- `service_unavailable` — the requested service is offline for that country

Best practices (brief)
- Always handle both success and error JSON responses.
- Use the `price` endpoint to estimate cost before attempting a charge.
- Cache service and country lists locally to avoid frequent calls.
- Add retry and timeout logic for network calls.
