# Recharge (recharge-payments)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Recharge (Recharge Payments) is a subscription and recurring-billing platform for e-commerce, most widely used on Shopify (with BigCommerce and custom-store support). Its public REST API at `https://api.rechargeapps.com` lets developers manage the full subscription lifecycle programmatically - subscriptions, customers, addresses, charges, orders, products, payment methods, onetimes, discounts, and webhook endpoints. The API is resource-oriented JSON over HTTPS, with cursor-based pagination and a leaky-bucket rate limiter.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/recharge-payments/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/recharge-payments/refs/heads/main/apis.yml)

## Access Model and Authentication

The Recharge API is a **merchant API, not an open/anonymous API**. Using it requires a Recharge merchant account on a paid plan (Starter, Plus, or Custom), typically connected to a Shopify store. However, the full API reference documentation is public at [developer.rechargepayments.com](https://developer.rechargepayments.com).

- **Auth:** a store **API token** passed in the `X-Recharge-Access-Token` header. Tokens are generated per store in the merchant portal (Apps and integrations) and scoped to specific resource permissions. Public/partner apps use OAuth to obtain per-store tokens.
- **Versioning:** the `X-Recharge-Version` header selects the API version. Supported versions are **`2021-11`** (recommended) and **`2021-01`**; if omitted, the account default is used.
- **Transport:** all requests are made over HTTPS to `https://api.rechargeapps.com`. Responses are JSON.
- **Rate limits:** a leaky-bucket limiter with a bucket of **40 requests** that leaks **2 requests/second**; overflow returns HTTP `429` (sleep at least 2 seconds and retry).
- **Events:** near-real-time notifications are delivered via **outbound webhooks** (server-to-endpoint HTTPS POST). There is **no public WebSocket API**.

## Tags

- Subscriptions
- Recurring Billing
- E-commerce
- Payments
- Shopify
- Retention

## Timestamps

- **Created:** 2026-07-10
- **Modified:** 2026-07-10

## APIs

### Recharge Subscriptions API

Create, list, retrieve, update, and delete recurring subscriptions, and drive the subscription lifecycle with action endpoints - change the next charge date, change address, cancel, and activate. Subscriptions define product, quantity, price, and order interval, and schedule the charges that generate future orders.

- **Human URL:** [https://developer.rechargepayments.com/2021-11/subscriptions](https://developer.rechargepayments.com/2021-11/subscriptions)
- **Base URL:** `https://api.rechargeapps.com`

#### Tags

- Subscriptions
- Recurring Billing
- Lifecycle

#### Properties

- [Documentation](https://developer.rechargepayments.com/2021-11)
- [API Reference](https://developer.rechargepayments.com/2021-11/subscriptions)
- [OpenAPI](openapi/recharge-payments-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/recharge-payments.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/recharge-payments.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Recharge Customers API

Manage customer records that own addresses, subscriptions, and payment methods - create, list, retrieve, update, and delete customers, and read a customer's upcoming delivery schedule and credit summary. Customers link Recharge records to the underlying store's external customer identifier.

- **Human URL:** [https://developer.rechargepayments.com/2021-11/customers](https://developer.rechargepayments.com/2021-11/customers)
- **Base URL:** `https://api.rechargeapps.com`

#### Tags

- Customers
- Accounts
- Delivery Schedule

#### Properties

- [API Reference](https://developer.rechargepayments.com/2021-11/customers)
- [OpenAPI](openapi/recharge-payments-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/recharge-payments.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/recharge-payments.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Recharge Orders API

List, retrieve, update, and delete orders generated from charges, plus RPC-style actions to clone an order or delay it. Orders represent the concrete fulfillment record that flows to the connected storefront after a charge processes successfully.

- **Human URL:** [https://developer.rechargepayments.com/2021-11/orders](https://developer.rechargepayments.com/2021-11/orders)
- **Base URL:** `https://api.rechargeapps.com`

#### Tags

- Orders
- Fulfillment
- Recurring

#### Properties

- [API Reference](https://developer.rechargepayments.com/2021-11/orders)
- [OpenAPI](openapi/recharge-payments-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/recharge-payments.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/recharge-payments.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Recharge Charges API

List and retrieve scheduled and processed charges, and act on queued charges - skip, unskip, process now, refund, and apply or remove a discount. Charges are the billing events that draw against a customer's payment method and produce orders on success.

- **Human URL:** [https://developer.rechargepayments.com/2021-11/charges](https://developer.rechargepayments.com/2021-11/charges)
- **Base URL:** `https://api.rechargeapps.com`

#### Tags

- Charges
- Billing
- Payments

#### Properties

- [API Reference](https://developer.rechargepayments.com/2021-11/charges)
- [OpenAPI](openapi/recharge-payments-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/recharge-payments.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/recharge-payments.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Recharge Products API

Create, list, retrieve, update, and delete products and their subscription defaults - the discount, order-interval, and cutoff rules that govern how a storefront product can be subscribed to. Products map to the connected store's external product identifiers.

- **Human URL:** [https://developer.rechargepayments.com/2021-11/products](https://developer.rechargepayments.com/2021-11/products)
- **Base URL:** `https://api.rechargeapps.com`

#### Tags

- Products
- Catalog
- Subscription Rules

#### Properties

- [API Reference](https://developer.rechargepayments.com/2021-11/products)
- [OpenAPI](openapi/recharge-payments-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/recharge-payments.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/recharge-payments.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Recharge Webhooks API

Register, list, retrieve, update, delete, and test webhook endpoints that receive event notifications - for topics such as subscription, charge, order, and customer changes - via server-to-endpoint HTTPS POST. Webhooks are Recharge's push mechanism; there is no public WebSocket surface.

- **Human URL:** [https://developer.rechargepayments.com/2021-11/webhooks_endpoints](https://developer.rechargepayments.com/2021-11/webhooks_endpoints)
- **Base URL:** `https://api.rechargeapps.com`

#### Tags

- Webhooks
- Events
- Notifications

#### Properties

- [API Reference](https://developer.rechargepayments.com/2021-11/webhooks_endpoints)
- [OpenAPI](openapi/recharge-payments-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/recharge-payments.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/recharge-payments.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/ReChargePayments)
- [LinkedIn](https://www.linkedin.com/company/rechargepayments)
- [Website](https://getrecharge.com)
- [Documentation](https://developer.rechargepayments.com)
- [Plans](plans/recharge-payments-plans-pricing.yml)
- [Rate Limits](rate-limits/recharge-payments-rate-limits.yml)
- [Fin Ops](finops/recharge-payments-finops.yml)
- [Blog](https://getrecharge.com/blog/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
