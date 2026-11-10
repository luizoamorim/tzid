# Authorization Check (D2)

> Draft, conceptual. Covers SOW D2 ("protected operation must enforce the
> authorization check onchain"); acceptance A3, A4.

> **Is `caller` allowed to perform `action` on `resource` for `identity`, now?**

Default answer: **no**.

## Authorized only if

1. `caller` is authenticated via Soroban `require_auth` (signature and replay
   protection). Without this, anyone could claim to be the delegate.
2. `identity` exists, and either:
   - `caller` is its controller (root authority, see A-1 in
     [authority.md](authority.md)), or
   - a grant exists with delegator = `identity`, delegate = `caller`, exact
     (`action`, `resource`) match, not revoked, and ledger time before
     `expires_at`.

The protected operation MUST abort when the answer is no.

## Expected results

| Case | Result | SOW |
|---|---|---|
| Valid grant, in scope | Authorized | A3 |
| Different action/resource | Denied: ScopeMismatch | A3 |
| No grant (incl. bound wallet without grant) | Denied: NoGrant | A3 |
| Past `expires_at` | Denied: Expired | A4 |
| Revoked | Denied: Revoked | A4 |
| Unknown identity / unauthenticated caller | Denied | — |

## Limitations

- Revocation applies from the ledger where it lands; it is not retroactive.
- Ledger time advances in steps of a few seconds.

## Open questions

| # | Question |
|---|---|
| Z-1 | Who calls `require_auth`: the registry or the protected operation? |
| Z-2 | Does the caller pass the grant ID, or does the registry look it up? |
| Z-3 | Boundary: proposed expired when `now >= expires_at`. |
| Z-4 | Typed errors (favored by "clear error handling") vs. boolean; assert vs. query API. |
| Z-5 | Archived storage entries must fail closed; verify on current Testnet protocol. |
