# DriverPass UML Portfolio Models

> **Portfolio note:** The diagrams on this page are portfolio reconstructions derived from my DriverPass requirements and modeling analysis. They are not presented as screenshots of the original course templates or as production-ready system specifications. Their purpose is to show how I translate requirements into structural and behavioral models.

## Modeling Focus

DriverPass has several important workflows, but lesson scheduling is one of the strongest examples because it connects customers, employees, packages, instructors, vehicles, reservations, validation rules, and audit history.

The models below focus on that workflow while also showing the larger object structure needed to support it.

## Use-Case Overview

This is a high-level functional overview rather than formal UML use-case notation.

```mermaid
flowchart LR
    Customer[Customer]
    Secretary[Secretary]
    Instructor[Instructor]
    Owner[Owner]
    IT[IT Officer]
    Payment[Payment Service]
    DMV[DMV Update Source]

    subgraph DriverPass[DriverPass System]
        Register[Register / Manage Customer]
        Package[Select Training Package]
        Pay[Process Payment]
        Schedule[Schedule / Modify / Cancel Lesson]
        Learn[Access Course Content]
        Test[Take Practice Tests]
        Notes[Record Lesson Notes]
        Reports[Generate Reports]
        Accounts[Manage Accounts & Access]
        Updates[Process DMV Updates]
    end

    Customer --> Register
    Customer --> Package
    Customer --> Pay
    Customer --> Schedule
    Customer --> Learn
    Customer --> Test

    Secretary --> Register
    Secretary --> Schedule

    Instructor --> Notes
    Owner --> Reports
    Owner --> Package
    IT --> Accounts
    IT --> Updates

    Pay <--> Payment
    Updates <--> DMV
```

## Structural Model: Core Class Diagram

The class model emphasizes shared user behavior, employee specialization, scheduling resources, package eligibility, testing, payments, and audit history.

```mermaid
classDiagram
    class User {
        +userId
        +username
        +passwordHash
        +status
        +authenticate()
        +resetPassword()
    }

    class Customer {
        +contactInformation
        +pickupLocation
        +dropoffLocation
        +remainingHours
        +viewProgress()
    }

    class Employee {
        +employeeId
    }

    class Secretary {
        +registerCustomer()
        +manageReservation()
    }

    class Instructor {
        +viewAssignments()
        +recordLessonNote()
    }

    class Owner {
        +downloadReport()
        +disablePackage()
    }

    class ITOfficer {
        +manageAccount()
        +blockAccess()
        +resetEmployeePassword()
    }

    class Package {
        +packageId
        +name
        +includedHours
        +active
        +disable()
    }

    class Reservation {
        +reservationId
        +date
        +startTime
        +endTime
        +status
        +pickupLocation
        +create()
        +modify()
        +cancel()
    }

    class Vehicle {
        +vehicleId
        +status
        +isAvailable()
    }

    class PracticeTest {
        +testId
        +name
    }

    class TestAttempt {
        +attemptId
        +timeTaken
        +score
        +status
    }

    class Payment {
        +paymentId
        +amount
        +status
        +authorize()
    }

    class LessonNote {
        +noteId
        +lessonTime
        +comments
    }

    class AuditEntry {
        +auditId
        +timestamp
        +action
    }

    User <|-- Customer
    User <|-- Employee
    Employee <|-- Secretary
    Employee <|-- Instructor
    Employee <|-- Owner
    Employee <|-- ITOfficer

    Customer "0..*" --> "1" Package : selects
    Customer "1" --> "0..*" Reservation : books
    Reservation "0..*" --> "1" Instructor : assigned
    Reservation "0..*" --> "1" Vehicle : assigned
    Reservation "1" --> "0..1" LessonNote : produces
    Customer "1" --> "0..*" TestAttempt : completes
    PracticeTest "1" --> "0..*" TestAttempt : has
    Customer "1" --> "0..*" Payment : makes
    User "1" --> "0..*" AuditEntry : creates
    Reservation "1" --> "0..*" AuditEntry : tracked by
```

## Behavioral Model: Schedule Driving Lesson Activity

This activity model follows the reservation rules identified in the requirements: the customer must have enough package hours, the customer/instructor/vehicle must all be available for the full two-hour session, and a successful change must create an audit record.

```mermaid
flowchart TD
    Start((Start)) --> Auth[Authenticate user]
    Auth --> Request[Enter requested date, time, pickup and drop-off]
    Request --> Validate{Required data valid?}

    Validate -- No --> Error1[Show validation message]
    Error1 --> Request

    Validate -- Yes --> Hours{Enough package hours?}
    Hours -- No --> RejectHours[Reject request and explain package-hour issue]
    RejectHours --> End((End))

    Hours -- Yes --> Check[Check customer, instructor and vehicle availability]
    Check --> Available{Full two-hour slot available?}

    Available -- No --> Alternatives[Show conflict and available alternatives]
    Alternatives --> Request

    Available -- Yes --> Assign[Assign instructor and vehicle]
    Assign --> Confirm[Display reservation summary for confirmation]
    Confirm --> Accepted{User confirms?}

    Accepted -- No --> End
    Accepted -- Yes --> Save[Create reservation and update schedule]
    Save --> Audit[Record user, timestamp and action]
    Audit --> Success[Display confirmation]
    Success --> End
```

## Behavioral Model: Schedule Driving Lesson Sequence

The sequence diagram shows the same reservation scenario from an interaction perspective. It makes the order of validation, data access, conflict checking, persistence, and audit logging explicit.

```mermaid
sequenceDiagram
    actor User as Customer / Secretary
    participant UI as Web Interface
    participant RS as Reservation Service
    participant PS as Package Service
    participant AS as Availability Service
    participant DB as Central Database
    participant AL as Audit Log

    User->>UI: Enter requested lesson date/time and locations
    UI->>RS: submitReservationRequest(request, user)

    RS->>PS: verifyRemainingHours(customer, 2 hours)
    PS->>DB: read package and progress data
    DB-->>PS: package eligibility / remaining hours
    PS-->>RS: eligibility result

    alt Insufficient package hours
        RS-->>UI: Reject request with explanation
        UI-->>User: Display package-hour message
    else Eligible
        RS->>AS: checkAvailability(customer, instructor, vehicle, slot)
        AS->>DB: query schedules and resource availability
        DB-->>AS: matching availability data
        AS-->>RS: availability result

        alt Scheduling conflict
            RS-->>UI: Return conflict + alternative slots
            UI-->>User: Display alternatives
        else Slot available
            RS->>DB: create reservation and resource assignments
            DB-->>RS: reservation saved
            RS->>AL: record creation(user, reservation, timestamp)
            AL->>DB: save audit entry
            DB-->>AL: audit saved
            RS-->>UI: reservation confirmed
            UI-->>User: Display confirmation
        end
    end
```

## Design Decisions Represented

- **Centralized validation:** reservation rules are checked before data is committed.
- **No double-booking:** customer, instructor, and vehicle availability must all be valid for the full two-hour lesson.
- **Role-aware workflows:** both customers and secretaries can initiate reservation activity, while other roles have narrower responsibilities.
- **Auditability:** successful reservation changes are associated with the user and timestamp that produced them.
- **Separation of responsibilities:** package eligibility, availability checking, reservation persistence, and auditing are represented as distinct responsibilities.
- **Object-oriented structure:** shared user behavior is inherited while specialized employee roles keep role-specific operations separate.

## Traceability to Requirements

These diagrams are based on requirements that call for:

- browser-based access for customers and employees;
- role-based permissions;
- customer and secretary reservation management;
- two-hour driving lessons;
- instructor and vehicle assignment;
- prevention of overlapping reservations;
- tracking of remaining package hours;
- practice-test and lesson-progress records;
- downloadable reporting;
- and audit history for reservation creation, modification, and cancellation.

The goal of these models is to provide a clear bridge from stakeholder requirements to an implementable software structure without implying that the modeled system has already been built.
