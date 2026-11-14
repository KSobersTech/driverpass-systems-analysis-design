# DriverPass Acceptance Criteria

## Purpose and Scope

These scenarios convert high-priority DriverPass requirements into observable outcomes that a product owner, developer, and tester could review together. They are proposed portfolio extensions derived from the requirements and models; they are not evidence that a production system has been implemented.

## Authentication and Access

### Successful role-based login

- **Given** an active user with valid credentials
- **When** the user signs in
- **Then** the system creates a protected session and displays the workspace permitted for that user's role
- **And** server-side authorization remains required for every protected operation

### Invalid or blocked login

- **Given** invalid credentials, a blocked account, or a deactivated account
- **When** a login is attempted
- **Then** access is denied without revealing which credential or account condition failed
- **And** the failed attempt is recorded according to the security policy
- **And** repeated failures trigger the configured protective control

## Lesson Scheduling

### Confirm an eligible reservation

- **Given** an authenticated customer or authorized secretary
- **And** the customer has at least two eligible package hours
- **And** the customer, an instructor, and a vehicle are available for the complete requested interval
- **When** a valid two-hour reservation is confirmed
- **Then** one reservation is committed with the selected customer, instructor, vehicle, time, and locations
- **And** an audit entry records the actor, action, reservation, and timestamp
- **And** no competing request can commit an overlapping assignment for any of the three scheduled resources

### Reject insufficient package hours

- **Given** a customer with fewer than two eligible hours
- **When** a reservation is requested
- **Then** the reservation is not created
- **And** no instructor or vehicle is assigned
- **And** the user receives an actionable explanation without exposure of unrelated account data

### Reject a scheduling conflict

- **Given** an overlapping reservation for the customer, instructor, or vehicle
- **When** another request attempts to reserve the same interval
- **Then** only one conflicting reservation may commit
- **And** the rejected request leaves no partial assignment or audit record that implies success
- **And** available alternatives may be returned without exposing another customer's information

### Modify a reservation

- **Given** an existing reservation and an authorized actor
- **When** the actor submits a valid change
- **Then** eligibility and availability are rechecked before the change commits
- **And** the original values remain intact if validation or persistence fails
- **And** the successful modification creates an audit entry containing the actor and timestamp

### Cancel a reservation

- **Given** an existing reservation eligible for cancellation under the configured policy
- **When** an authorized actor confirms cancellation
- **Then** the reservation changes to the appropriate canceled state rather than disappearing from history
- **And** instructor and vehicle availability is released
- **And** package-hour treatment follows the approved cancellation rule
- **And** an audit entry is created

## Packages and Payments

### Hide a disabled package from new sales

- **Given** an owner has disabled a package
- **When** a new customer views purchasable packages
- **Then** the disabled package is not offered for purchase
- **And** historical purchases, lessons, and reports retain their original package reference

### Handle an approved payment

- **Given** a valid package purchase and an approved response from the payment provider
- **When** the transaction is finalized
- **Then** the purchase is recorded exactly once
- **And** the customer's package entitlement becomes available according to the business rule
- **And** full payment credentials are not stored by DriverPass

### Handle a declined or interrupted payment

- **Given** a declined, timed-out, or interrupted provider response
- **When** the purchase cannot be confirmed
- **Then** no active entitlement is granted
- **And** retry or reconciliation cannot create a duplicate charge or duplicate purchase
- **And** the customer receives a safe, actionable status

## Training and Progress

### Record a practice-test attempt

- **Given** a customer with access to the selected practice test
- **When** the test is submitted
- **Then** the test identifier, customer, elapsed time, score, completion status, and timestamp are recorded
- **And** the score and duration satisfy the configured validation rules
- **And** an unauthorized customer cannot read another customer's attempt

### Record a completed lesson

- **Given** an assigned instructor and a scheduled lesson
- **When** the instructor records the completed time and comments
- **Then** the lesson note is associated with the correct reservation and customer
- **And** package progress is adjusted no more than once
- **And** unauthorized roles cannot create or alter the instructor's record

## Administration and Reporting

### Manage account access

- **Given** an authenticated IT officer
- **When** an account is blocked, deactivated, reset, or restored
- **Then** the new access state is enforced on subsequent protected requests
- **And** an audit record identifies the administrator, target account, action, and timestamp
- **And** an unauthorized role cannot perform the operation

### Download a report

- **Given** an owner authorized for the selected report
- **When** valid filters are submitted
- **Then** the exported data matches those filters and the user's permissions
- **And** empty results produce a valid empty report rather than an error
- **And** untrusted values are escaped safely in the export format

## Cross-Cutting Completion Criteria

A workflow is not ready for acceptance unless:

- Server-side authorization is enforced.
- Required fields and business rules are validated.
- Failure does not leave partial persistent state.
- Sensitive values are not exposed in messages or logs.
- Successful material changes create the required audit history.
- User-facing error messages explain what can be corrected.
- Relevant accessibility behavior is verified against the selected standard.
- Tests cover normal behavior, expected invalid states, and important concurrency or retry risks.

