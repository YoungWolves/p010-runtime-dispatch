# P010 Runtime Dispatch

This repository is a non-authoritative dispatch bus for **P010 — The Sentinel**.

Durable authority remains in the relevant project's authoritative Google Drive records. Nothing in this repository, a pull request, branch, commit, issue, or comment independently grants lifecycle or mutation authority.

## Purpose

P010 may publish a bounded `EFFECTOR_EXECUTION_PACKET` here after the controller has resolved and fresh-revalidated the relevant durable authorization. A configured external Work effector may be triggered by the resulting GitHub event and carry that packet to the authorised target surface.

## Safety model

- Repository events are **dispatch signals**, not authority.
- The current packet must carry an explicit authorization/delegation reference and idempotency key for mutation-capable work.
- The effector must fail closed on ambiguity, expiry, scope mismatch, stale revisions, consumed authorization, or missing target-owned preconditions.
- The effector must not mint or broaden authorization.
- TinyFish/browser automation must not substitute for the external Work effector where Work browser/computer execution is required.
- Target-project lifecycle and canonical mutation remain governed by the target project's authoritative protocol/delegation.

## Test sequence

1. Configure the P010 Effector Surface Work task to trigger on pull-request activity from this repository.
2. Open the prepared no-op dispatch pull request.
3. The Work effector should wake automatically, recognize `OPERATION=DISPATCH_TEST_NO_TARGET_MUTATION`, and report receipt without mutating any target project.
4. Only after that handshake passes should a fresh, controller-generated Culture execution packet be dispatched through the same path.
