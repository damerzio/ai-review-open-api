---
seo:
  title: Example Shop API documentation
  description: Reference documentation for the Storefront and Inventory APIs.
---

# Example Shop API documentation

Two API descriptions live in this project.

- **[Storefront API](./apis/storefront/openapi.yaml)** — the public catalog, cart and
  checkout API used by the shop front end. OpenAPI 3.1.
- **[Inventory API](./apis/inventory/openapi.yaml)** — the internal warehouse system of
  record. OpenAPI 3.0.

Both descriptions reuse one component library in `apis/shared/components`, so a change to
an error payload or a rate-limit header lands in every operation at once.
