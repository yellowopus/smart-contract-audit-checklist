# Smart Contract Audit Checklist

A checklist for auditing smart contracts in a bug bounty program — from
intake to a filed report. Drawn from audit work on DeFi programs
(stablecoins, staking, and vaults).

This repo summarizes **methodology only**. It does not contain any audit
report, any program's private data, or any finding. Apply it to programs
you are authorized to audit.

## The workflow in one paragraph

Intake the scope and read the docs. Set up a local fork and test there —
never on mainnet or a public testnet unless the program explicitly
allows it. Enumerate candidates (functions, invariants, trust
boundaries), triage each one to a verdict, prove the survivors with a
minimal proof-of-concept on the fork, pass the 7-question gate, and only
then file.

## Contents

| File | What it is |
| --- | --- |
| [CHECKLIST.md](CHECKLIST.md) | Copy-paste checklists for every phase |
| [WORKFLOW.md](WORKFLOW.md) | Intake, fork setup, triage, Slither/Foundry |
| [POC-STANDARD.md](POC-STANDARD.md) | What a proof-of-concept must prove |

## Hard rules

1. **Local forks only** unless the program says otherwise. Never test
   on mainnet. Never spend real funds to prove a finding.
2. **Only your own funds and your own accounts** in any test.
3. **Read the docs before the code.** A function that looks wrong is
   often documented behavior.
4. **Report only what you can prove on the fork** with a minimal PoC.
5. **Check for known issues first.** Most "new" findings are variants
   of documented ones.

## License

MIT — see [LICENSE](LICENSE).
