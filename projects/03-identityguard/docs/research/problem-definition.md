# Problem definition — IdentityGuard

**Status:** draft hypothesis, not a validated client case.

## Context

A **fictional** medium-sized business with approximately **300 synthetic employees** uses multiple applications. Some access is granted and removed through manual Service Desk requests. The precise departments, roles and application inventory will be defined in Phase 1 after the project owner approves the next phase.

## Core problem statement

**When staff join, move, or leave**, identities and downstream accounts can become inconsistent with current job responsibilities. Manual and fragmented approvals may delay provisioning, retain unnecessary access, leave accounts enabled after termination, and make auditor requests costly to reconstruct.

## Four core risks

| ID | Symptom (hypothetical) | Business risk | Candidate control | Proof to plan |
|---|---|---|---|---|
| P-01 | New joiner waits for required access | Reduced productivity; manual workload | Policy-based baseline role provisioning | Time from event to expected access |
| P-02 | Mover retains former department permissions | Least-privilege violation | Role recalculation and revoked old entitlements | Before/after role comparison |
| P-03 | Leaver account remains active | Unauthorized post-employment access | Automated revocation and reconciliation | Negative check for active target accounts |
| P-04 | Approval cannot be reconstructed | Weak accountability/audit readiness | Logged request/approval/action chain | Actor, timestamp, justification and result |

## Stakeholders (hypotheses)

- **HR:** source owner for personnel status events.
- **IAM / IT:** operational control owner for provisioning and deprovisioning.
- **Line manager / application owner:** business approver for role-sensitive access.
- **Information security / GRC:** policy owner, exception reviewer, audit liaison.
- **Employee:** access requester or subject.

The financial sponsor/budget approver **is not established** by the source research and varies across companies.

## Proposed outcome

Build a **reproducible laboratory**, not a commercial product, that proves (1) correct baseline provisioning, (2) timely access retirement, (3) transparent decisions, and (4) detection of residual inappropriate access using fabricated data.

## Measurement principles

Baseline and outcomes will be generated or measured **in a laboratory**. No fabricated loss savings or customer impact. Monetary models, if developed, will publish assumptions and formulas separately.

## Open questions (Phase 0)

1. Which specific controls are essential for the first MVP?
2. What is the minimum testable identity-and-entitlement model?
3. Which event and evidence fields must be retained?
4. What functionality must be intentionally excluded for scope and budget reasons?
