# Preliminary requirements traceability

**Status:** Phase 0 candidate requirements; final priorities and acceptance thresholds still require review. Planned tests are **not executed**.

| Requirement ID | Business problem | Planned capability | Acceptance test (future) | Evidence (future) | Priority |
|---|---|---|---|---|---|
| IAM-001 | P-01 onboarding delays | Create synthetic identity from authoritative HR event and assign role-based baseline access | Valid Joiner event produces only the defined entitlements | Input event, entitlement diff and event log | MUST |
| IAM-002 | P-02 mover retains access | Re-evaluate role assignments on department/position change | Former job permissions are removed; new baseline appears | Before/after permissions | MUST |
| IAM-003 | P-03 leaver retains access | Disable identity and revoke all managed access on Leaver event | No managed target account remains active for that person | Revocation results and reconciliation | MUST |
| IAM-004 | P-04 decisions not auditable | Record identity/access actions and result | Each operation has an actor, UTC timestamp, action, target and outcome | Exportable audit event | MUST |
| IAM-005 | Excessive/inconsistent permissions | Compare entitlements to approved role policy | At least one deliberate excess entitlement is detected in synthetic test data | Policy test report | SHOULD |
| IAM-006 | Unapproved sensitive access | Request/approval gate before high-risk entitlement | Unapproved request cannot be provisioned | Rejected request and decision trail | SHOULD |
| IAM-007 | Unsynchronized downstream state | Compare desired and observed target access | Deliberate mismatch is reported, not silently ignored | Reconciliation report | SHOULD |
| IAM-008 | Unreviewed access over time | Review campaign with revoke decision | Completed review generates decision and revocation evidence | Certification report | LATER |
| IAM-009 | SoD conflicts | Detect prohibited permission combinations | Synthetic dual-role conflict is flagged | SoD check report | LATER |

## Requirement quality rules

- Every item must map to a business problem (P-xx), an observable condition and test evidence.
- No acceptance test may be marked passed before implementation and execution.
- Every policy or threshold needs an explicit owner and rationale.
- Vendor-specific functionality is optional until access and licensing are confirmed.

## Decision pending

Confirm the four **MUST** controls (IAM-001 through IAM-004) as the initial candidate MVP; this is a Phase 0 proposal, not implemented architecture.
