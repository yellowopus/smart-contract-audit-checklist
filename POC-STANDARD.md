# Proof-of-Concept Standard

A PoC is not a demo. It is the evidence that turns a hypothesis into a
reportable finding. Every PoC in this workflow must meet this standard.

## What a PoC must show

1. **The setup** — fork state, contracts, accounts, and starting
   balances. A triager must be able to reproduce it from a clean fork.
2. **The steps** — the smallest sequence of calls that triggers the
   issue. Numbered, no extra calls.
3. **Before and after state** — balances, allowances, roles, or
   cooldowns, shown before the trigger and after it. The difference is
   the finding.
4. **The impact** — whose funds or whose account is affected, and what
   action the attacker can take. Concrete, not theoretical.
5. **The boundary** — what the PoC does **not** show. If it only works
   for the attacker's own funds, say so (and kill the finding).

## Rules

- **Fork-local only.** All calls run on the local fork. No mainnet, no
  public testnet, no real funds.
- **Only your own accounts.** The PoC must not touch any other user's
  funds, data, or account.
- **Minimal.** If a step can be removed without changing the result,
  remove it. A 3-step PoC is stronger than a 30-step one.
- **Deterministic.** Same fork state, same result, every run. Pin the
  fork block if the behavior depends on chain state.
- **No secrets.** No private keys, no RPC keys with quota, no personal
  data in the PoC or the report.

## PoC template (Foundry test)

```solidity
// Minimal PoC: <one-sentence description of the issue>
// Setup: fork at block <N>, attacker = <role>, victim = <role>
// Expected: <what should happen>
// Observed: <what actually happens>
```

Write the test so that it **fails** on the vulnerable code and
**passes** once the issue is fixed. That is the strongest form of
evidence: the test itself defines the fix.

## What a PoC is not

- Not a long exploit chain with ten preconditions. If it needs ten
  preconditions, the impact is usually theoretical.
- Not a mainnet transaction. Never.
- Not a screenshot. Screenshots supplement a PoC; they never replace it.
