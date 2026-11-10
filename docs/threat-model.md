# Threat Model

> Living document. Mitigations are planned, not implemented.

**Scope:** `contracts/`, `go/`, `scripts/` on Stellar Testnet.
**Assumptions:** Stellar consensus, Soroban host and `require_auth` behave as
specified; ledger time is approximately correct; controllers protect their
keys.

## Threats

| ID | Threat | Planned mitigation |
|---|---|---|
| T1 | Unauthorized controller change | Require current controller authorization (I-3). |
| T2 | Unauthorized wallet binding | Require controller (and possibly wallet) authorization (I-5). |
| T3 | Front-running a chosen identity ID | Non-claimable ID generation (I-1). |
| T4 | Personal data onchain or in fixtures | No free-form fields; synthetic fixtures; review. |
| T5 | Wallet correlation via public bindings | Inherent; documented. |
| T6 | Grant exceeds controller-defined authority | Only controller grants; no re-delegation (A-2). |
| T7 | Revoked/expired grant becomes valid (incl. storage archival) | Terminal revocation; fail closed (A-6, Z-5). |
| T8 | Bound wallet acts without a grant | Relationship ≠ Permission; tested (A3). |
| T9 | Check without authenticated caller (confused deputy) | Bind check to `require_auth`; protected operation aborts (Z-1). |
| T10 | Expiration off-by-one | Defined boundary; tests on both sides (Z-3). |
| T11 | Delegate acts in the same window as revocation | Inherent; documented. |
| T12 | Audit history lost | Never delete grants; emit events (A4). |
| T13 | Admin/upgrade key compromise | Decide ARCH-2. |
| T14 | Keys committed or wrong network used | `.gitignore`; explicit Testnet passphrase. |
| T15 | Trusting RPC simulation as final | Confirm included transaction results. |
| T16 | Dependency compromise | Pinned versions and lock files. |

## Review findings

Required by A6: no unresolved critical/high findings.

| ID | Severity | Finding | Status |
|---|---|---|---|
| — | — | No review performed yet. | — |
