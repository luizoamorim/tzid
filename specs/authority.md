# Delegated Authority (D2)

> Draft, conceptual. Covers SOW D2; acceptance A3, A4. Check semantics:
> [authorization.md](authorization.md).

An identity grants an address narrow, time-bound, revocable authority.

## Grant

| Field | Description |
|---|---|
| `delegator` | Identity granting authority, acting through its controller. |
| `delegate` | Address receiving authority. |
| `action` | Application-defined verb (e.g. `transfer`). |
| `resource` | Application-defined opaque reference. |
| `expires_at` | After this, the grant is invalid. |
| `revoked` | Set by the delegator; terminal. |

Scopes match **exactly** (no wildcards) in Sprint 1.

## Operations

| Operation | Authorization |
|---|---|
| Grant | Delegator's controller |
| Revoke | Delegator's controller |
| Read | Public |

Grant fails if: unauthorized, `expires_at` not in the future, unknown
delegator, or scope beyond the controller-defined authority.

## Non-escalation

Grants cannot exceed the controller-defined authority. If only the controller
can grant (no re-delegation), this holds by construction — the proposed
Sprint 1 option.

## Invariants

1. Revoked or expired grants are never valid again.
2. Grants are never deleted; history remains auditable via storage and events (A4).
3. No personal data in grants.

## Open questions

| # | Question |
|---|---|
| A-1 | How is the controller's authority over a resource established? TZID does not know resource semantics. |
| A-2 | Re-delegation in Sprint 1? Proposed: no. |
| A-3 | Types for `action` and `resource`. |
| A-4 | Time unit for `expires_at`: ledger timestamp or sequence. |
| A-5 | Duplicate grants, maximum lifetime, delegate renouncing a grant. |
| A-6 | Storage TTL: archival must never revive a revoked grant, and history must stay auditable. |

Out of scope: identity-to-identity delegation, wildcard scopes, conditional
limits, offchain delegation tokens.
