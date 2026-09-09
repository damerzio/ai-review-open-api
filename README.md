# ai-review-open-api

Test fixture repository for the AI reviewer. It holds two multi-file OpenAPI
descriptions that share one component library, so a pull request can exercise the
reviewer against realistic `$ref` graphs.

## Layout

```
apis/
  shared/components/     schemas, headers, responses and parameters used by both APIs
  storefront/            public catalog, cart and checkout API (OpenAPI 3.1)
    openapi.yaml
    paths/
    components/schemas/
  inventory/             internal warehouse API (OpenAPI 3.0)
    openapi.yaml
    paths/
    components/schemas/
redocly.yaml             registers both API roots
```

Two OpenAPI versions on purpose: `additionalProperties` behaves differently in 3.0 and
3.1, and several lint rules are version specific.

## Baseline

The descriptions are deliberately close to compliant: TLS-only servers, an audience
declared with `x-internal`, non-empty security on every operation, documented `400`,
`401`, `429` and `500` responses with bodies, rate-limit and CORS headers, bounded
strings, arrays and integers.

Three known gaps are left in place so that a review can be seen to ignore findings
outside the lines a pull request touches:

- `apis/inventory/components/schemas/Supplier.yaml` — `notes` has no `maxLength`.
- `apis/inventory/paths/warehouses.yaml` — `listWarehouses` documents no `429`.
- `apis/storefront/paths/oauth2_token.yaml` — the token endpoint is intentionally
  unauthenticated and declares `security: []`.
