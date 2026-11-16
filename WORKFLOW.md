# Workflow

## 1. Intake

- List every in-scope contract with its chain and address, from the
  program page — not from memory.
- Read the documentation before the code: specs, docs site, and NatSpec
  comments. A function that looks wrong is often documented behavior,
  and a function that looks right can still break an invariant the docs
  state.
- Review known issues and previous findings for the same codebase. Most
  "new" findings are variants of documented ones — check first, so you
  do not spend a day proving something already known.
- Note the severity guidance: what the program pays for, and what it
  explicitly does not pay for.

## 2. Local fork setup

- Clone the program's repositories (public ones only).
- Configure a local fork of the target chain (Foundry `forge` with a
  fork URL from a public RPC endpoint). All testing happens on the fork.
- Fund test accounts with fork-local tokens only. Never use real funds,
  never test on mainnet, never test on a public testnet unless the
  program explicitly allows it.
- Confirm the fork matches the deployed code: compare the deployed
  bytecode against the local build where possible. If the deployed code
  differs from the repo (for example, a pre-fix version), note it —
  auditing the wrong version wastes the whole engagement.

## 3. Static analysis

Run Slither over the in-scope contracts first. It is fast and catches
the mechanical issues:

```sh
slither <contract-dir> --exclude-dependencies
```

- Triage every finding: most Slither output is informational. Record
  which findings you checked and why each one is or is not an issue.
- Use Slither to build a map, not just a list: which functions change
  which state, which are access-controlled, which touch funds.

## 4. Candidate enumeration

List candidates as one-sentence hypotheses, for example:

- "A restricted user can bypass a cooldown after a seizure."
- "An admin function can be called by an unauthorized role."
- "A rounding error lets a user extract more than their share."

For each candidate, note: who can call it, what state it changes, who
is affected, and whether the behavior is documented.

## 5. Triage

Kill candidates fast:

- **Documented behavior** — the docs say it works this way. Killed.
- **Self-only impact** — the "attacker" can only harm their own funds
  or their own account. Killed (programs do not pay for self-harm).
- **Known issue / variant** — matches a documented issue or a previous
  finding. Killed, or noted as a variant with the difference stated.
- **Unreachable** — the precondition cannot happen on the fork (for
  example, it requires an admin action that the program controls).
  Killed.
- **Needs PoC** — survives triage. Build the proof.

A triage log that shows 20 candidates killed and 1 proven is more
valuable than a report that hides the kills.

## 6. Prove on the fork

See [POC-STANDARD.md](POC-STANDARD.md). A finding without a working PoC
on the fork is a hypothesis, not a report.

## 7. File

Only after the 7-question gate passes (see CHECKLIST.md). Use the
program's report form, state severity with reasoning, attach the PoC,
and disclose honestly what you tested and what you did not test.

## 8. After filing

- Save the report ID and the PoC in your own notes.
- Answer triager questions with evidence, not new claims.
- If the report is judged a duplicate or invalid, record why — it is
  triage data for the next engagement.
- Never re-test a fixed issue on production without permission.
