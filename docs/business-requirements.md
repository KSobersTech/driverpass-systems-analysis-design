# DriverPass Business Requirements

## Purpose
DriverPass is a driver-training company created to improve preparation for state driving tests. The proposed system combines online learning, practice testing, package enrollment, payment, lesson scheduling, progress tracking, and business reporting in one web-based platform.

The system is designed for multiple user groups, including customers, secretaries, driving instructors, the owner, and IT personnel, with role-based access appropriate to each user.

## System Goals

- Provide a centralized browser-based system available from desktop and mobile devices.
- Allow customers to register, purchase a training package, access learning content, take practice tests, and manage driving lessons.
- Allow staff to register customers and manage reservations.
- Prevent double-booking of customers, instructors, or vehicles.
- Track package hours, practice-test performance, lesson history, and instructor comments.
- Provide downloadable business and activity reports.
- Maintain role-based permissions and an audit history of important changes.
- Support approved DMV content updates.

## Nonfunctional Requirements

### Performance
- Common actions such as login, progress lookup, availability checks, and reservation changes should complete without unnecessary delay.
- Reservation changes must be committed immediately to prevent conflicting bookings.
- The hosting environment should support backup, monitoring, recovery, and growth.

### Platform
- Responsive web application.
- Compatible with current desktop and mobile browsers.
- Centralized database for users, roles, packages, reservations, vehicles, instructors, test results, notes, and audit records.
- Shared data changes require an online connection.
- Backend integrations should support secure payment processing and authorized DMV update sources.

### Accuracy and Data Integrity
- Unique identifiers for major business records.
- Validation of required fields, dates, times, payment input, addresses, and package eligibility.
- Availability checks before confirming lessons.
- Audit records for reservation creation, modification, and cancellation.

### Adaptability
- User accounts, roles, permissions, and status should be configurable without source-code changes.
- Existing packages can be disabled without deleting historical records.
- Course content and practice questions should remain separate from application code so they can be updated efficiently.

### Security
- Unique user authentication.
- Role-based access control.
- Encrypted client-server communication.
- Secure password hashing.
- Protection against repeated failed-login attempts.
- Secure password reset.
- Third-party payment processing rather than storing full payment credentials.
- Session controls, audit logging, least privilege, backups, and monitoring.

## Functional Requirements

The system shall:

- Validate credentials and display the appropriate role-based dashboard.
- Allow IT personnel to create, modify, reset, block, and deactivate accounts.
- Allow secure password reset.
- Store customer contact information, locations, package information, payment status, and progress.
- Display available DriverPass training packages.
- Allow the owner to disable packages for new purchases.
- Process payments through a secure payment service.
- Allow customers and authorized staff to create, modify, and cancel driving lessons.
- Schedule lessons in two-hour blocks.
- Assign available instructors and vehicles.
- Prevent overlapping reservations.
- Track completed and remaining package hours.
- Provide course content and practice tests based on package access.
- Record test name, time taken, score, and completion status.
- Allow instructors to record lesson times and comments.
- Provide downloadable business, progress, and activity reports.
- Record who created, modified, or canceled a reservation and when.
- Receive approved DMV rules, policy, and sample-question updates.
- Provide customer-contact functionality.

## User Interface Requirements

The interface should be responsive and browser-based.

### Customers
- Registration
- Login and password reset
- Package selection and payment
- Lesson scheduling
- Course content and practice tests
- Progress review
- Driver notes
- Contact tools

### Secretary
- Customer registration
- Availability lookup
- Reservation creation and modification

### Driving Instructor
- Assigned lesson view
- Lesson-time and comment entry

### Owner
- Business dashboards
- Activity reports
- Package, reservation, progress, instructor, and vehicle reporting

### IT Officer
- Account administration
- Roles and permissions
- Access status
- System notifications
- Update management

## Assumptions

- Users have internet access and a supported browser when modifying shared data.
- A managed cloud provider supplies hosting, monitoring, backup, recovery, and baseline infrastructure security.
- DriverPass will use an authorized DMV update source when available.
- A third-party payment processor will handle sensitive payment credentials.
- DriverPass will define remaining business rules such as cancellation windows, refunds, retention, and notification timing before implementation is finalized.

## Limitations

- Shared data cannot be safely modified offline.
- The first release can disable existing packages, but adding or removing entire package modules requires future development.
- Lesson availability is constrained by instructor schedules, vehicle availability, two-hour blocks, and package entitlements.
- DMV updates depend on an external source outside DriverPass control.
- Availability and recovery depend partly on selected cloud and payment providers.
- Final budget, SLA, accessibility standard, retention policy, and detailed legal/compliance requirements require additional stakeholder confirmation.

---

This portfolio version is adapted from my CS 255 DriverPass Business Requirements Document and is intended to demonstrate requirements analysis and systems-design skills.