# Security Policy

TZID is pre-release, unaudited and targets **Stellar Testnet only**. Do not use
it to protect real value.

## Reporting a vulnerability

**Do not report vulnerabilities in public issues, pull requests or
discussions.**

Use **GitHub private vulnerability reporting** (Security tab → *Report a
vulnerability*). If unavailable, open a public issue asking only for a private
contact channel, with no technical details. A dedicated security contact will
be published here once defined.

Please include: affected component, commit hash, impact, reproduction steps
(ideally a test case or Testnet transaction hash) and any suggested fix.

We handle reports on a best-effort basis, coordinate disclosure with the
reporter and credit them with consent. There is no bug bounty.

## Scope

**In scope:** `contracts/`, `go/`, `scripts/`, and unsafe behavior specified in
`specs/`.

**Out of scope:** Stellar Core, Soroban, Stellar RPC, Stellar CLI and other
third-party dependencies (report upstream); attacks requiring a compromised
controller key; social engineering; denial of service against public
infrastructure.

## Good-faith research

Test only on Testnet or locally, with accounts you control, without affecting
others' data or shared infrastructure, and allow time for a fix before
disclosure. We will not pursue action against researchers who follow this
policy.
