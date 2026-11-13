# MVP scope — Phase 0 proposal

**Status:** proposal for review (not yet baseline-approved).

## In scope for initial MVP

1. Synthetic personnel records and identity lifecycle events (Joiner, Mover, Leaver).
2. Small policy-driven RBAC role and entitlement catalog.
3. Simulation of provisioning and deprovisioning for one or more local *mock* applications.
4. Audit evidence for each decision and state transition.
5. Positive and negative test scenarios for initial controls.
6. Simple measurable KPIs, reported honestly as lab findings once tested.

## Deferred to later phases

- Access requests and approvals; access certification campaigns.
- Orphan account and excessive permission analytics; SoD policy engine.
- SCIM/REST/LDAP/Keycloak integrations and reconciliation with live targets.
- Dashboards, operational alerts, extensive resilience testing.

## Explicitly excluded from MVP

- Production SailPoint or Microsoft Entra Governance dependencies.
- Real employee data or real customer systems.
- Enterprise production deployment, commercial SLA, or penetration testing of third parties.
- Homegrown implementation of OAuth 2.0 / OIDC cryptography.
- PAM/JIT, AI-agent identities, complex frontend and enterprise-scale performance commitments.

## Technical restrictions (proposal)

- Budget: prefer zero additional licensing cost and local execution on Linux.
- Vendor access: never assume enterprise evaluation tenant availability.
- Security: synthetic data, no secrets committed, least privilege, sanitized logs.
- Documentation: English outward-facing materials; Spanish learning notes.

## Definition of MVP done (future)

- IAM-001 through IAM-004 pass tests in a reproducible, documented environment.
- At least one happy-path and one failure/negative-path test for each core control.
- Evidence demonstrates role changes and effective revocation across *managed mock targets*.
- README, setup instructions, known limitations, test log and sample walkthrough are complete.
- The project owner approves the MVP after a walkthrough.

**Important:** this is the intended end-of-MVP acceptance gate, not the Phase 0 exit gate.
