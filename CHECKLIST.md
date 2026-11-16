# Checklists

## Intake

- [ ] Program page read in full (scope, rules, rewards, KYC)
- [ ] In-scope contracts listed (addresses + which chain)
- [ ] Out-of-scope items listed
- [ ] Testing rules noted (local fork only? no mainnet? no testnet?)
- [ ] Documentation read (docs site, specs, NatSpec comments)
- [ ] Known issues / previous findings reviewed
- [ ] Reward table and severity guidance noted

## Setup

- [ ] Repo cloned; dependencies installed
- [ ] Local fork configured (fork URL from a public RPC endpoint)
- [ ] Foundry toolchain working (`forge build` passes)
- [ ] Slither installed and running on the in-scope contracts
- [ ] Test wallet funded with fork-local tokens only (never real funds)

## Triage (per candidate)

- [ ] Function / invariant written down in one sentence
- [ ] Who can call it, and with what permissions?
- [ ] What state does it change, and who is affected?
- [ ] Is the behavior documented? (If yes, it is probably not a bug.)
- [ ] Checked against known issues / previous findings?
- [ ] Verdict: killed / needs PoC / proven

## Proof of concept

- [ ] Minimal PoC on the local fork (smallest steps that show the issue)
- [ ] PoC uses only my own accounts and fork-local funds
- [ ] Before/after state shown (balances, allowances, roles)
- [ ] Impact stated concretely (whose funds, what action)
- [ ] PoC is reproducible from a clean fork state

## Before filing (7-question gate)

- [ ] In scope
- [ ] Authorized (fork-local, own funds only)
- [ ] Reproducible
- [ ] Real impact
- [ ] Not a duplicate or a known-issue variant
- [ ] Evidence attached (PoC + before/after state)
- [ ] No secrets in the report
