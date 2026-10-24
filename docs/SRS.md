# Software Requirements Specification

## Campus Canteen Ordering System

| Document field | Value |
|---|---|
| Version | 1.0 |
| Status | Draft for classroom review |
| Last updated | 2026-10-24 |

## 1. Introduction

### 1.1 Purpose

This Software Requirements Specification (SRS) defines what the Campus Canteen Ordering System must do and the conditions it must satisfy. It gives students, canteen staff, stakeholders, designers, developers, and testers a shared basis for implementation and acceptance. Each requirement has a unique identifier that can be referenced in issues, design work, and tests.

The SRS describes required system behavior without prescribing a programming language, framework, database, or deployment design.

### 1.2 Scope

The system supports the initial educational prototype's campus canteen ordering workflow. Students can view the menu, choose items and quantities, review a calculated total, submit an order, and view its status. Canteen staff can review and process incoming orders by updating their status.

Payment is simulated; real payment processing and payment-gateway integration are out of scope. Off-campus delivery, advanced stock forecasting, accounting integration, and order cancellation are also out of scope for this baseline. The cancellation policy remains undecided and must be agreed with stakeholders before a cancellation workflow is added.

### 1.3 Intended readers

- Students placing orders.
- Canteen staff reviewing and processing orders.
- College or canteen administration overseeing the service and menu.
- The development team specifying, implementing, testing, and maintaining the system.

### 1.4 Definitions

| Term | Definition |
|---|---|
| Student | A customer using the prototype to browse the menu and place or track an order. |
| Menu item | A food or drink entry with a name, price, and availability; a short description may also be provided. |
| Order | A selection of one or more menu items and quantities submitted by a student. |
| Order reference | A value shown as confirmation and used to identify an order. |
| Staff | An authorized canteen worker who reviews and processes orders. |
| Simulated payment | A prototype representation of payment that does not make a real payment transaction. |

## 2. Overall description

### 2.1 Product context

The system provides a digital ordering workflow between students and the campus canteen. Menu and order data may be simulated in the earliest version. No particular storage, user-interface technology, or authentication mechanism is assumed by this specification.

### 2.2 User classes

- **Student:** Views the menu, selects available items, submits orders, and views the status of their own orders.
- **Canteen staff:** Reviews incoming orders and updates their statuses.
- **College or canteen administration:** Oversees the service and may maintain menu information. The role allowed to add, edit, or disable menu items requires stakeholder confirmation.
- **Development team:** Uses requirement IDs to plan and verify implementation.

### 2.3 Assumptions and constraints

- Only available menu items may be ordered.
- Quantities are positive whole numbers, and an order must contain at least one item.
- The order total is the sum of each unit price multiplied by its quantity. Taxes and service charges are excluded from the initial prototype.
- The initial order statuses are **Submitted**, **Preparing**, **Ready**, and **Completed**.
- The prototype must not process real payments.
- Authentication and authorization details must be designed before real student information is used.
- The performance target in Section 5 is provisional and must be confirmed with stakeholders and tested in a documented environment.

## 3. Functional requirements

The following requirements define the mandatory functional baseline and shall be verified against their stated acceptance criteria.

### 3.1 Menu

| ID | Requirement | Acceptance criteria |
|---|---|---|
| FR-001 | The system shall display menu items with their names, prices, and availability. It may display a short description when one is available. | Given that menu items exist, each displayed item has a name and price; unavailable items are clearly identified. |

### 3.2 Selection and order total

| ID | Requirement | Acceptance criteria |
|---|---|---|
| FR-002 | The system shall allow a student to select available menu items and specify a positive whole-number quantity for each selected item. | A student can select more than one available item; a zero, negative, fractional, unknown, or unavailable item is rejected. |
| FR-003 | The system shall calculate and display the order total as the sum of each selected item's unit price multiplied by its quantity. Taxes and service charges shall not be included in the initial prototype total. | The displayed total matches the itemized calculation and is recalculated when an item or quantity changes; an empty order or invalid quantity is rejected. |

### 3.3 Order submission

| ID | Requirement | Acceptance criteria |
|---|---|---|
| FR-004 | The system shall allow a student to submit a valid order containing at least one available item and shall provide an order confirmation or reference. Any payment represented by the initial prototype shall be simulated; the system shall not process a real payment. | A valid order can be submitted; an empty or invalid order cannot; successful submission displays a confirmation or reference that reflects the submitted order; no real payment transaction is made. |

### 3.4 Order status

| ID | Requirement | Acceptance criteria |
|---|---|---|
| FR-005 | The system shall allow a student to view the current status of their own order. | An order has a recognizable status; the student can view their own order's status but cannot view or change another student's private order. |
| FR-006 | The system shall allow authorized canteen staff to review incoming orders and update their status to Submitted, Preparing, Ready, or Completed. | Staff can review an order and change its status to one of the defined statuses; the updated status is reflected when the student views that order again. |

## 4. Business rules

| ID | Rule |
|---|---|
| BR-001 | Only available menu items can be included in an order. |
| BR-002 | Each ordered quantity must be a positive whole number. |
| BR-003 | An order must contain at least one item. |
| BR-004 | The initial prototype total is the sum of item prices multiplied by quantities; taxes and service charges are excluded. |
| BR-005 | The initial order statuses are Submitted, Preparing, Ready, and Completed. |
| BR-006 | Payment is simulated; real payment processing is outside the initial scope. |
| BR-007 | Order cancellation is not part of the baseline because the cancellation policy has not been agreed. |

## 5. Non-functional requirements

The performance target in this section is provisional for a classroom exercise, not a measured production guarantee. The test environment and workload must be defined and documented before the result can be assessed.

| ID | Requirement | Acceptance criteria |
|---|---|---|
| NFR-001 | Under a defined test environment with 50 concurrent virtual users, 95% of menu requests shall complete within 2 seconds. This target is provisional and must be confirmed before use in a real setting. | A performance test report records the environment, workload, measured 95th-percentile response time, and comparison with the target. |
| NFR-002 | The system shall prevent a student from viewing or changing another student's private order. Authorized canteen staff shall be able to access orders needed for processing, subject to the system's approved permissions. | A student can access their own order; attempts to access another student's order by changing an identifier or URL are rejected without exposing its details; unauthorized order changes are rejected; authorized staff can access orders needed for processing. |

## 6. Requirements validation and traceability

### 6.1 Validation

Before implementation or acceptance, stakeholders should review each requirement for correctness, necessity, clarity, consistency, feasibility, and testability. Validation should include:

- Walking through the menu, item selection, quantity changes, order-total calculation, submission, and status-tracking scenarios.
- Testing that unavailable items, invalid quantities, and empty orders are rejected.
- Testing that a student can access their own order but cannot view or change another student's private order.
- Testing that authorized staff can review orders and update their statuses.
- Measuring menu response times using the workload and environment agreed for NFR-001.
- Confirming that the simulated payment does not trigger a real transaction.

### 6.2 Open questions for stakeholder review

- At what point, if any, may a student cancel an order?
- Which role may add, edit, or disable menu items?
- What authentication and authorization approach will be approved before real student information is used?
- Who approves the performance target and test environment?
- Can simulated menu and order data be used throughout the initial prototype?

### 6.3 Traceability and change control

Requirement IDs are stable references for GitHub Issues, design work, implementation, and tests. Each issue or test should cite the requirement ID it addresses. If a requirement changes without changing its meaning, retain its ID; assign a new ID to a new requirement. Stakeholder-approved changes to scope or acceptance criteria must be reflected in this SRS before they are treated as part of the baseline.
