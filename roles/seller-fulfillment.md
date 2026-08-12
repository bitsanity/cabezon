# Seller fulfillment model

The Seller role uses **fulfillment** as the common operation for delivering a
physical good, a digital result, or both.

This model does not change who controls funds. The Escrower remains authoritative
for the order, payment, bond, timeout, dispute, and release state. A Seller's
fulfillment descriptor is evidence presented to the buyer and Escrower; it is not
proof that the buyer accepted the result or that the offering met every claim.

## Fee separation

Three values must not be conflated:

1. The `purchase` CARP service fee admits the request and deters abusive traffic.
2. The offering price is the value charged for the good or service.
3. The Escrower's `buy` amount can include the offering price, buyer bond, and
   escrow fee.

Paying the admission fee does not pay for the order.

## Lifecycle

1. A buyer discovers a Seller through CABEZON.
2. The buyer calls `enquiry` for free and receives matching offerings.
3. The buyer calls `purchase`, paying any declared admission fee.
4. The Seller validates the selection and returns an order ID plus Escrower
   payment instructions.
5. The buyer calls the Escrower's `buy` service.
6. After payment is confirmed, the Seller fulfills the order.
7. The Seller calls the Escrower's existing `ship` service with a fulfillment
   reference. A carrier tracking number remains valid. A digital Seller can use
   a result ID or URI identifying a typed fulfillment descriptor.
8. The buyer verifies delivery and calls the Escrower's `confirm` service, or
   uses timeout/arbitration when applicable.
9. The Escrower releases funds according to its contract.

Each offering should publish a delivery deadline and the remedy available when
that deadline is missed. A Seller may describe the remedy, but only the Escrower
or an applicable Arbitrator authorizes release, refund, or bond disposition.

Suggested order states are `PAYMENT_REQUIRED`, `PAID`, `FULFILLING`,
`FULFILLED`, `COMPLETED`, `TIMEDOUT`, and `ARBITRATION`. The Escrower's state is
authoritative when it differs from a Seller's local state.

## Compatibility

The services `about`, `enquiry`, and `purchase` are retained.

- `itemref` and `upc` map to `offeringRef`.
- `shipto` maps to `delivery.destination`.
- Sellers adopting version 0.2 should accept both the documented object parameters
  and the `legacy-params` form during the compatibility period.
- A plain tracking number remains a valid fulfillment reference.
- A richer descriptor is optional and can be addressed by the reference string.

## Safety and privacy

- Treat enquiry and purchase fields as untrusted input.
- Use `clientOrderRef` as an idempotency key so retries do not create duplicate
  orders.
- Do not place credentials, private customer data, source documents, or digital
  result content in a public fulfillment descriptor.
- Prefer opaque retrieval references plus cryptographic digests.
- A content digest proves byte identity, not correctness, quality, or buyer
  acceptance.
- Retrieval URLs should be HTTPS, narrowly scoped, and time limited.

See [`examples/seller-physical.json`](examples/seller-physical.json) and
[`examples/seller-digital.json`](examples/seller-digital.json).
