# DriverPass Requirements Traceability Matrix

## Purpose

This matrix connects DriverPass stakeholder needs to design evidence and a proposed verification method. It makes gaps visible before implementation begins and prevents a diagram or technical decision from drifting away from the client requirement it is intended to support.

> **Status key:** **Covered** means the portfolio design addresses the requirement. **Partial** means important detail remains unresolved. **Open** means stakeholder or implementation decisions are still required. These statuses describe design coverage, not deployed functionality.

## Functional Requirements

| ID | Requirement | Design evidence | Proposed verification | Status |
|---|---|---|---|---|
| AUTH-01 | Authenticate users and display the correct role-based workspace | User hierarchy and role-specific operations in the [UML models](uml-models.md); security requirements in the [requirements summary](business-requirements.md) | Valid, invalid, blocked, and deactivated login scenarios; authorization tests for every protected operation | Covered |
| ACCT-01 | Allow IT personnel to create, modify, reset, block, and deactivate accounts | `ITOfficer` operations in the class model | Role-restricted account lifecycle tests with audit verification | Covered |
| CUST-01 | Store customer contact, location, package, payment, and progress information | Customer, Package, Payment, Reservation, and TestAttempt concepts in the structural model | Create/update validation, persistence, authorization, and retrieval tests | Covered |
| PKG-01 | Display available training packages | Package entity and customer package-selection relationship | Only active packages appear to new customers | Covered |
| PKG-02 | Allow the owner to disable packages without deleting history | Package `active` state and `disable()` behavior | Disabled package is unavailable for new purchases while historical enrollments remain readable | Covered |
| PAY-01 | Process payments without storing full payment credentials | External payment-service boundary and third-party processing requirement | Approved, declined, duplicate, timeout, and retry scenarios; verify sensitive payment credentials are not persisted | Partial |
| RES-01 | Create, modify, and cancel lessons | Reservation class plus activity and sequence models | Authorized customer and secretary workflows, validation failures, and audit checks | Covered |
| RES-02 | Schedule lessons in two-hour blocks | Activity and sequence models; reservation start/end data | Reject durations or boundaries that violate the two-hour rule | Covered |
| RES-03 | Assign an available instructor and vehicle | Reservation-to-Instructor and Reservation-to-Vehicle relationships | Confirm both resources are available for the complete interval before commit | Covered |
| RES-04 | Prevent overlapping customer, instructor, and vehicle reservations | Central availability check in activity and sequence models | Concurrent conflict tests at each resource boundary | Covered |
| PROG-01 | Track completed and remaining package hours | Customer progress and package eligibility checks | Completed lesson adjusts entitlement once; cancellation and failed completion do not consume hours incorrectly | Partial |
| LEARN-01 | Provide course content according to package access | Course and package-access requirements | Authorized package grants content; inactive or insufficient access is denied | Partial |
| TEST-01 | Record practice-test name, duration, score, and completion status | PracticeTest and TestAttempt classes | Persist complete attempt data and reject invalid scores or durations | Covered |
| INST-01 | Allow instructors to record lesson time and comments | LessonNote entity and Instructor operation | Assigned instructor can add a note; unrelated users cannot | Covered |
| RPT-01 | Provide downloadable business, progress, and activity reports | Owner reporting operation and reporting requirement | Role authorization, filter accuracy, export format, empty results, and large-result behavior | Partial |
| AUD-01 | Record who created, modified, or canceled a reservation and when | AuditEntry relationships and explicit audit step in activity/sequence models | Immutable audit entry created in the same successful operation as each reservation change | Covered |
| DMV-01 | Receive approved DMV rules, policy, and question updates | External DMV update-source boundary | Verify source authenticity, validation, versioning, failure recovery, and approval workflow | Open |
| CONTACT-01 | Provide customer-contact functionality | Requirement identified in the business summary | Stakeholder must select channels, consent rules, templates, and delivery provider before design is complete | Open |

## Nonfunctional Requirements

| ID | Quality attribute | Design response | Proposed verification | Status |
|---|---|---|---|---|
| SEC-01 | Authentication and authorization | Unique accounts, password hashing, role-based access, session controls, least privilege | Authentication, session-expiry, privilege-escalation, and authorization test suite | Covered |
| SEC-02 | Protected communications and payments | TLS for client/server traffic; external payment provider; no full payment credentials stored | Transport configuration review and data-storage inspection | Covered |
| DATA-01 | Accuracy and integrity | Unique identifiers, validation, transactional reservation checks, and audit history | Constraint tests, rollback tests, concurrency tests, and migration tests | Covered |
| PERF-01 | Responsive common operations | Centralized services and indexed relational queries are proposed | Define measurable response-time targets and validate with representative load | Partial |
| REL-01 | Backup, monitoring, and recovery | Managed hosting, backup, monitoring, and recovery responsibilities are identified | Restore exercise, recovery-time/recovery-point validation, alert tests | Partial |
| COMP-01 | Desktop and mobile browser support | Responsive browser-based interface | Supported-browser matrix and responsive-layout testing | Covered |
| A11Y-01 | Accessible user experience | Accessibility checks are recommended in the portfolio reflection | Select a target standard and verify keyboard, focus, semantics, contrast, zoom, and assistive-technology behavior | Open |
| PRIV-01 | Responsible retention and privacy | Least privilege and protected data are identified | Stakeholder decisions are required for retention, deletion, consent, and applicable legal obligations | Open |

## Highest-Priority Open Decisions

1. Define cancellation windows, refunds, rescheduling rules, and no-show behavior.
2. Decide whether package hours are reserved at booking or consumed only after lesson completion.
3. Select payment and DMV integration contracts, including retry and reconciliation behavior.
4. Define notification channels, consent, delivery timing, and failure handling.
5. Set measurable availability, performance, backup, and recovery objectives.
6. Select an accessibility target and supported browser/device matrix.
7. Establish data-retention, deletion, and privacy requirements.

## Maintenance Rule

Every material requirement change should update this matrix, the affected model or contract, and the corresponding acceptance criteria in the same review. A requirement is not considered implementation-ready while its business rule or verification method remains ambiguous.

