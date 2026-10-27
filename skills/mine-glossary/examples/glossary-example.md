# E-Commerce & Subscription Platform Domain Glossary & Ubiquitous Language

<!-- Invariant: All paths must be repository-relative or enclosed in inline code backticks. NEVER use file:// or workstation-absolute paths (/Users/*, /home/*). -->

## Purpose & Scope
This living document maintains the canonical Ubiquitous Language across all platform packages (`packages/core`, `packages/billing`, `packages/fulfillment`). All specifications, contracts, and code comments must strictly adhere to these definitions.

---

## 1. Order Fulfillment & Payments

- **Order**:
  - **Bounded Context**: Order Fulfillment (`packages/core/types/order.ts`)
  - **Code Anchor**: `Order` in `packages/core/types/order.ts`
  - **Localized Synonyms (zh-TW)**: 訂單 / 採購單
  - **Forbidden Aliases**: cart, checkout_basket, bill
  - **Domain Invariant**: An order transitions through `PENDING` ➔ `CONFIRMED` ➔ `FULFILLED` or `CANCELLED`. Only confirmed orders can be fulfilled.

- **Cancel**:
  - **Bounded Context**: Order Fulfillment (`packages/core/types/order.ts`)
  - **Code Anchor**: `OrderStatus.CANCELLED` in `packages/core/types/order.ts`
  - **Localized Synonyms (zh-TW)**: 取消 / 取消訂單
  - **Forbidden Aliases**: refund, void, terminate, delete
  - **Domain Invariant**: Terminates an order before payment capture or fulfillment dispatch without financial ledger reversal. Distinct from `Refund`.

- **Refund**:
  - **Bounded Context**: Billing & Payments (`packages/billing/src/types/refund.ts`)
  - **Code Anchor**: `RefundTransaction` in `packages/billing/src/types/refund.ts`
  - **Localized Synonyms (zh-TW)**: 退款 / 沖退
  - **Forbidden Aliases**: cancel, void, chargeback
  - **Domain Invariant**: Reverses captured funds back to the customer payment method, generating an audited negative balance entry. Only captured transactions can be refunded.

---

## 2. Subscriptions & Licensing

- **Subscription**:
  - **Bounded Context**: Subscription Management (`packages/billing/src/types/subscription.ts`)
  - **Code Anchor**: `UserSubscription` in `packages/billing/src/types/subscription.ts`
  - **Localized Synonyms (zh-TW)**: 訂閱 / 訂閱方案
  - **Forbidden Aliases**: membership, recurring_order, plan_license
  - **Domain Invariant**: Represents an ongoing recurring billing relationship (`ACTIVE`, `PAST_DUE`, `CANCELED`). Cancellation does not immediately revoke access until the current billing period expires.

- **Seat**:
  - **Bounded Context**: Licensing & Access (`packages/core/types/licensing.ts`)
  - **Code Anchor**: `OrganizationSeat` in `packages/core/types/licensing.ts`
  - **Localized Synonyms (zh-TW)**: 授權席位 / 使用者席位
  - **Forbidden Aliases**: user, account, slot, license
  - **Domain Invariant**: An allocated license slot assigned to an individual user within an organization. Reassigning a seat does not modify organization billing total.
