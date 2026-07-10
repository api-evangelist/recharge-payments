# Recharge (recharge-payments)

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
