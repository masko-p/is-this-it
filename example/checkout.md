# Checkout Promo Codes

A sample specification for intent review. Some details are deliberately left open so the preview can make the questions visible.

## User Story

As a customer checking out, I want to apply a promotional code from an email so that I can receive the intended discount and understand the final amount before placing my order.

## Context

Customers should be able to recover from promo-code errors without losing their cart or the code they entered. Discount information should remain visible through order confirmation.

## Acceptance Criteria

1. **AC1 - Code entry.** Checkout provides a labeled promo-code field and an action to apply it.
2. **AC2 - Valid code.** Applying a valid code to an eligible cart immediately updates the visible discount and total.
3. **AC3 - Expired or invalid code.** Reject expired or invalid codes with an informative error. Do not apply a discount, and keep totals accurate.
4. **AC4 - Ineligible cart.** Do not apply a discount when the cart is ineligible. Explain the outcome to the customer.
5. **AC5 - One-time use.** A redeemed one-time code cannot be reused. Show an informative error when it is rejected.
6. **AC6 - Discount visibility.** Show the applied discount in both the checkout summary and the final order confirmation.
7. **AC7 - Duplicate prevention.** Applying the same code again must not apply its discount twice or change the total again.
8. **AC8 - Validation failure.** Redirect appropriately if validation fails, preserving the cart and a path back to checkout.
9. **AC9 - Recovery.** Handle errors gracefully, retain the entered code, and allow the customer to continue checkout without a discount.
10. **AC10 - Auditability.** Promo-code validation and redemption outcomes must be auditable.
11. **AC11 - Performance.** Checkout must remain responsive under standard load.

## Open Questions

- What is the promotion value, and does it apply to shipping?
- Which rules make a cart eligible?
- Does "validation fails" in AC8 mean rejected codes, a service failure, or both? What is the redirect destination?
- May different promo codes be combined or replace one another? AC7 only defines repeated application of the same code.
- What must an audit record contain, and how long is it retained?
- What load and response-time targets define AC11?

## Preview Fixtures

These values make the example readable; they are not product rules:

- Cart: a beach towel for $44, a linen tote for $28, and a sun hat for $36. Subtotal: $108.
- Shipping: $8. Initial total: $116.
- Entered code: `SUMMER-EMAIL`. A successful example uses an illustrative $18 discount, giving a $98 total.
- The reviewer can select a simulated validation outcome: valid, expired, invalid, ineligible, already redeemed, or service unavailable. The outcome is independent of the entered code.

## Scope

Render the customer-facing checkout, recovery, and confirmation surfaces. Mark eligibility checks, one-time redemption enforcement, duplicate prevention across requests, audit storage, and load performance as backend behavior that a local HTML preview cannot verify.

Promotion management, payment processing, and an audit viewer are outside this example.
