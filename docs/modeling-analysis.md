# DriverPass Modeling Analysis

## Process Model Application

A process model helps show how information moves through DriverPass and what the system must do at each point. The main external actors include the customer, secretary, driving instructor, owner, IT officer, payment service, and DMV update source.

Major processes include:

- Managing accounts
- Registering customers
- Processing payments
- Scheduling lessons
- Delivering online training
- Recording practice-test results
- Maintaining lesson notes
- Producing reports

### Example: Lesson Reservation

A customer or secretary enters a requested date and time. The system checks the customer's remaining package hours and compares the request with instructor and vehicle availability. If the full two-hour period is available, the system creates the reservation, assigns the instructor and vehicle, updates the schedule, and records who made the reservation.

A modification or cancellation follows a related workflow and creates an audit entry. If a conflict exists, the system should reject the invalid reservation and offer another available time rather than saving conflicting data.

Process models are especially useful for registration, password reset, package selection, practice testing, DMV content updates, and report generation because they make workflow steps and data exchanges visible to both technical and nontechnical stakeholders.

## Object Model Application

An object model approaches DriverPass by identifying the people, records, and system resources that need to exist.

Potential classes include:

- User
- Customer
- Employee
- Secretary
- Instructor
- Owner
- ITOfficer
- Account
- Role
- Package
- Reservation
- Vehicle
- Payment
- Course
- PracticeTest
- TestAttempt
- LessonNote
- Report
- AuditEntry

### Example: Reservation Object

A `Reservation` could contain:

- Date
- Start time
- End time
- Status
- Pickup location
- Customer
- Instructor
- Vehicle

It would also support behaviors such as creating, modifying, and canceling a reservation.

### Relationships and OOP Principles

A customer can have multiple reservations and test attempts. Each reservation connects one customer, one available instructor, and one available vehicle for a two-hour session. A practice test can have many attempts, while each attempt belongs to one customer and stores its own score, elapsed time, and status.

Inheritance can reduce duplication. `Customer` and `Employee` can inherit shared account behavior from `User`, while `Secretary`, `Instructor`, `Owner`, and `ITOfficer` can specialize employee behavior and permissions.

Encapsulation can protect business rules by requiring data changes through approved methods. For example, a reservation object could reject scheduling conflicts, while an account object could enforce password-reset and access-status rules.

## Process vs. Object Modeling

### Process Modeling Strengths
- Shows the complete workflow from request to response.
- Helps business stakeholders identify missing steps.
- Works well for registration, payment, scheduling, testing, and reporting.

### Process Modeling Tradeoffs
- Can repeat similar data across several diagrams.
- Does not describe internal software structure as clearly.
- Large systems can require many related process diagrams.

### Object Modeling Strengths
- Defines reusable software concepts and relationships.
- Maps naturally to object-oriented implementation.
- Makes ownership, responsibility, and multiplicity clearer.

### Object Modeling Tradeoffs
- A class model alone does not show the order in which users complete tasks.
- It can be more technical for business stakeholders.
- Poor class choices early in design can make later changes harder.

## Recommended Approach

For DriverPass, I would begin with process modeling because the stakeholder interview is primarily expressed in terms of what users need to accomplish. After validating those workflows with the client, I would use object modeling to define the software structure that supports them.

Using both perspectives creates a useful cross-check: every important process should be supported by the right objects, and every major object should exist to serve a real business process.

---

This portfolio version is adapted from my CS 255 Model Application Short Paper and is intended to demonstrate process modeling, object modeling, and object-oriented systems analysis.