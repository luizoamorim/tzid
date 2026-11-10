# Identity (D1)

> Draft, conceptual. Covers SOW D1; acceptance A1, A2.

A persistent, opaque identity independent from any single key, bound to
controller addresses and wallets, with no personal data onchain.

## Model

| Field | Description |
|---|---|
| `id` | Opaque, unique, never reused. MUST NOT be derived from personal data (hashes of low-entropy data are reversible). |
| `controller` | Address(es) allowed to manage the identity. Classic (`G…`) or contract account (`C…`); contract accounts provide multisig/recovery. |
| `wallets` | Addresses bound to the identity. |

## Operations

| Operation | Authorization |
|---|---|
| Register identity | Controller |
| Bind wallet | Controller (proposed: also the wallet, I-5) |
| Unbind wallet | Controller |
| Change controller | Current controller |
| Read | Public |

Every change MUST fail without the required authorization and SHOULD emit an
event.

## Invariants

1. Changing wallet bindings or controllers never changes `id` (Identity ≠ Wallet).
2. A bound wallet has no authority to act for the identity by itself
   (Relationship ≠ Permission).
3. No personal data in storage. Bindings are public and correlate wallets.

## Open questions

| # | Question |
|---|---|
| I-1 | How is `id` generated? Counter (enumerable), client-chosen (front-runnable) or derived from controller + salt. |
| I-2 | One controller or several? The SOW says "controller addresses". |
| I-3 | Does changing controller also require the new controller's signature? |
| I-4 | Can a wallet unbind itself? Can it be bound to several identities? Max wallets per identity? |
| I-5 | Require the wallet's own signature when binding? Beyond SOW A2; prevents claiming third-party wallets. |
| I-6 | Identity deactivation in Sprint 1? |
| I-7 | Storage TTL and event schema. |
