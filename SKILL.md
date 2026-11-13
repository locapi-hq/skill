---
name: locapi
description: Call the LocAPI geolocation API for place search, nearby and reverse geocoding, addresses, postal codes, timezones, IP lookup, boundaries, and distance matrices. Use when the user asks for coordinates, a place name, a Czech address, or a distance between places.
---

# LocAPI

LocAPI is the geolocation API at `https://locapi.dev`. Use the hosted MCP server when the client can attach a remote MCP server. Otherwise call the REST API. Both use the customer's API key and the same credits.

Never invent a key, never put a key in a URL, and never send a request to `localhost`.

## 1. Get a key

The user creates a key in the LocAPI console at `https://locapi.net/console/api-keys` and stores it as `LOCAPI_API_KEY`. If that variable is missing, ask the user for it. Do not continue with a guessed key.

## 2. Prefer MCP

Endpoint: `https://locapi.dev/mcp/geo`
Header: `Authorization: Bearer <LOCAPI_API_KEY>`
Transport: Streamable HTTP

`tools/list` returns `search_tools` and `execute_tools`. Discover the operation with `search_tools`, then call it through `execute_tools`. The operation names include `search_locations`, `nearby_locations`, `reverse_geocode_location`, `search_addresses`, `get_timezone`, `geolocate_ip`, and `calculate_distance_matrix`.

A call is done when the tool result contains the place, address, or distance the user asked for, including coordinates.

## 3. REST when MCP is unavailable

Origin: `https://locapi.dev`
Header: `Locapi-Api-Key: <LOCAPI_API_KEY>`
Paths start with `/api/v1`. Health is `/api/health`.

| Need | Request |
| --- | --- |
| Place by name | `GET /api/v1/locations?q=Prague` |
| Places near a point | `GET /api/v1/locations/nearby?latitude=50.08&longitude=14.42` |
| Geo search | `GET /api/v1/locations/geo-search?latitude=50&longitude=14` |
| Czech address | `GET /api/v1/addresses?q=Přílucká&countryCode=CZ` |
| Timezone | `GET /api/v1/timezones?lat=50.08&lon=14.42` |

Send query parameters in camelCase. Read `success`, `error`, and `message` on failure. `402` means the subscription is inactive. `429` means the credit or rate limit is spent. Stop and tell the user. Do not retry a `402`.

Programmer reference: `https://locapi.dev/api/docs`. OpenAPI: `https://locapi.dev/api/docs.openapi`.

## 4. Official SDKs

- JavaScript: `npm install @locapi/sdk` (`0.3.0` or newer). The client appends `/api`.
- PHP: `composer require locapi/sdk` (`0.3.0` or newer). Pass the origin only, `https://locapi.dev`.
