# DriverPass Systems Analysis & Design

This repository contains my CS 255 portfolio work for the DriverPass project. It shows how I moved from listening to a client's needs to documenting requirements and designing a system that a development team could build.

## Required Portfolio Artifacts

| Course artifact | Description |
|---|---|
| [Project One: Business Requirements Document](Keishmar_Sobers_DriverPass_Business_Requirements.docx) | The client requirements, business goals, functional and nonfunctional requirements, assumptions, limitations, security needs, and project schedule |
| [Project Two: System Design Document](Keishmar_Sobers_CS255_Project_Two_System_Design.docx) | The system design, UML diagrams, technical requirements, security decisions, constraints, and requirement-to-design alignment |

## Portfolio Reflection

### Briefly summarize the DriverPass project. Who was the client, and what type of system did they want?

The client was DriverPass, a driver-training company owned by Liam. DriverPass wanted a web-based system that would give customers one place to register, purchase a training package, access online classes and practice tests, schedule driving lessons, and track their progress. The system also needed tools for the secretary, instructors, owner, and IT officer to manage appointments, accounts, reports, training content, and daily business operations.

### What did you do particularly well?

I think I did especially well at taking the information from the DriverPass interview and turning it into clear requirements and system models. I did not only list features. I connected the client's needs to user roles, scheduling rules, security controls, package-hour limits, and the way information should move through the system. My diagrams also show how different parts of DriverPass work together instead of treating every feature as a separate piece.

### If you could revise one part of your work, what would you improve?

If I could revise one part, I would spend more time validating the diagrams with people representing each DriverPass user role. A customer, secretary, instructor, owner, and IT officer may each notice different missing steps or confusing parts. I would use their feedback to simplify the diagrams where possible and make sure every important exception, such as a declined payment or unavailable lesson time, is represented clearly.

### How did you interpret the user's needs and implement them into the system design? Why is that important?

I interpreted the user's needs by looking beyond what each person asked for and thinking about why they needed it. For example, scheduling a lesson is not only choosing a date and time. The system must also check the customer's remaining package hours, instructor availability, vehicle availability, and possible conflicts before confirming the appointment. Considering the user's needs is important because a system can work technically and still fail if it does not support how people actually perform their jobs.

### How do you approach designing software? What strategies would you use in the future?

My approach is to understand the problem before deciding on the technology. I start by identifying the users, their goals, the business rules, and the information the system must protect. I then break larger processes into smaller workflows and use requirements, use cases, activity diagrams, sequence diagrams, and class diagrams to view the system from different angles. In future projects, I would continue using this process while adding more stakeholder reviews, prototypes, requirement traceability, accessibility checks, and early testing so problems can be corrected before they become expensive to fix.

## Supplemental Portfolio Material

- [Business Requirements Summary](docs/business-requirements.md)
- [Modeling Analysis](docs/modeling-analysis.md)
- [UML Portfolio Models](docs/uml-models.md)
- [Project Schedule](docs/project-schedule.md)

## Skills Demonstrated

- Systems analysis and requirements gathering
- Functional and nonfunctional requirements
- Unified Modeling Language (UML)
- Object-oriented analysis and design
- Process, structural, and behavioral modeling
- Security and role-based access planning
- Technical documentation
- Software Development Life Cycle planning

## AI Use Acknowledgment

ChatGPT (OpenAI, 2026) was used to help organize the assignment requirements, review the project documents, and revise the reflection for clarity. I reviewed the final content and verified it against the DriverPass interview, my completed course documents, and the portfolio instructions.

---

**Keishmar Sobers**  
Computer Science Student | Software Engineering Concentration  
Healthcare Technology | Software Development
