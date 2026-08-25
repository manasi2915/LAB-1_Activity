# Pharmacy Expiry & Re-order Dispatch Engine

## Requirements Engineering & UML Use-Case Modelling — Lab 1

**Problem Statement #15 — Healthcare & Telemedicine**
**Department of Computer Science & Engineering, PES University**

---

##  Problem Overview

Hospital pharmacies need an automated stock management system that tracks medicine batch expiry dates, generates **First-Expired-First-Out (FEFO)** dispensing lists, and automatically triggers purchase orders when medicine stock reaches or falls below the configured safety threshold.

The system is designed to support pharmacy staff in maintaining correct batch rotation, reducing medicine wastage, and ensuring timely re-ordering.

### Primary Actors

* **Pharmacy Clerk** — Registers medicine batches, dispenses medicines, and generates FEFO picking lists.
* **System Scheduler** — Monitors medicine stock levels for threshold breaches.
* **Inventory Supplier** — Acknowledges and updates the status of dispatched purchase orders.

---

##  Objectives

The objectives of this lab are to:

* Elicit and document functional and non-functional requirements.
* Define clear and measurable acceptance criteria.
* Identify system actors and use cases.
* Model system behavior using a UML Use-Case Diagram.
* Demonstrate `«include»` and `«extend»` relationships.
* Specify the main success scenario and alternate flows for a core use case.
* Apply structured Software Requirements Specification (SRS) practices.

---

##  Requirements

The system contains exactly **5 Functional Requirements** and **2 Non-Functional Requirements**.

### Functional Requirements

| ID         | Requirement                                                                                                                                                               |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **FR-001** | The system shall enforce FEFO picking order by prioritizing medicine batches with the nearest expiry date during sales checkout.                                          |
| **FR-002** | The system shall allow a Pharmacy Clerk to register a new medicine batch by recording batch ID, medicine name, quantity received, and expiry date.                        |
| **FR-003** | The system shall generate a FEFO-ordered dispensing/picking list for a given medicine, showing all in-stock batches sorted by ascending expiry date.                      |
| **FR-004** | The system shall detect when a medicine's available stock falls at or below its configured safety threshold and flag the medicine for re-order processing.                |
| **FR-005** | The system shall allow an Inventory Supplier to update the status of a dispatched purchase order and update the corresponding expected-incoming-stock record accordingly. |

### Non-Functional Requirements

| ID          | Requirement                                                                                                                                                    |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **NFR-001** | The system shall automatically generate and dispatch supplier purchase order requests when item stock dips below the safety threshold.                         |
| **NFR-002** | The system shall maintain an immutable audit log of batch registration, dispensing transactions, and purchase-order events, retained for a minimum of 3 years. |

---

##  Use Cases

The system is modelled using the following use cases:

* **UC-01 — Register Medicine Batch**
* **UC-02 — Dispense Medicine**
* **UC-03 — Select Earliest-Expiring Batch**
* **UC-04 — Generate FEFO Picking List**
* **UC-05 — Monitor Stock Levels**
* **UC-06 — Generate Purchase Order**
* **UC-07 — Dispatch Purchase Order**
* **UC-08 — Acknowledge Purchase Order**

### UML Relationships

#### `«include»`

* **Dispense Medicine** `«include»` **Select Earliest-Expiring Batch**
* **Generate FEFO Picking List** `«include»` **Select Earliest-Expiring Batch**
* **Generate Purchase Order** `«include»` **Dispatch Purchase Order**

#### `«extend»`

* **Generate Purchase Order** `«extend»` **Monitor Stock Levels**

The purchase order generation is conditional because it occurs when monitored medicine stock falls at or below the configured safety threshold.

---

##  Core Use-Case Flow

### UC-02 — Dispense Medicine

**Primary Actor:** Pharmacy Clerk

**Goal:**
Dispense the correct medicine batch while following FEFO order and selecting the oldest valid, unexpired batch first.

### Preconditions

* Pharmacy Clerk is logged into the system.
* The requested medicine has at least one unexpired batch in stock.

### Main Success Scenario

1. Pharmacy Clerk selects **Dispense Medicine** and enters the medicine name and requested quantity.
2. The system retrieves all in-stock batches of the medicine.
3. The system selects the oldest unexpired batch first according to FEFO order.
4. The system deducts the requested quantity from the selected batch or batches, continuing in FEFO order if necessary.
5. The system logs the dispensing transaction.
6. The system displays confirmation to the Pharmacy Clerk.
7. The use case ends successfully.

### Alternate Flows

**3a. No Valid Unexpired Batch Exists**

* The system finds that all batches are expired or out of stock.
* The system displays a "No valid batch available" message.
* The transaction is blocked.

**4a. Total Available Stock Is Insufficient**

* The system determines that the combined quantity across all unexpired batches is less than the requested quantity.
* The system displays the maximum available quantity.
* The Pharmacy Clerk may dispense the available quantity or cancel the transaction.

---

##  Repository Contents

```text
.
├── README.md
├── Requirements_Table.docx
├── UseCase_Diagram.pdf
└── UseCase_Flow.docx
```

### Files

| File                      | Description                                                                                                |
| ------------------------- | ---------------------------------------------------------------------------------------------------------- |
| `Requirements_Table.docx` | Complete functional and non-functional requirements table                                                  |
| `UseCase_Diagram.pdf`     | UML Use-Case Diagram containing actors, use cases, associations, `«include»`, and `«extend»` relationships |
| `UseCase_Flow.docx`       | Detailed use-case flow for UC-02 — Dispense Medicine                                                       |

---

##  Tools Used

* **Draw.io** — UML Use-Case Diagram
* **Microsoft Word** — Requirements Table and Use-Case Flow
* **GitHub** — Repository and submission

---

##  Lab Learning Outcomes

This lab demonstrates the ability to:

1. Write clear and testable functional requirements.
2. Define measurable non-functional requirements.
3. Identify actors and system use cases.
4. Construct UML Use-Case Diagrams.
5. Correctly use `«include»` and `«extend»` relationships.
6. Document main and alternate use-case flows.
7. Structure requirements according to SRS principles.

---

##  Actors & Responsibilities

| Actor                  | Responsibility                                                                     |
| ---------------------- | ---------------------------------------------------------------------------------- |
| **Pharmacy Clerk**     | Registers medicine batches, dispenses medicines, and generates FEFO picking lists. |
| **System Scheduler**   | Initiates stock-level monitoring.                                                  |
| **Inventory Supplier** | Acknowledges and updates purchase-order status.                                    |

---

##  Submission

This repository contains the complete deliverables for **Lab 1: Requirements Engineering & UML Use-Case Modelling**, based on **Problem Statement #15 — Pharmacy Expiry & Re-order Dispatch Engine**.

All requirements, use cases, relationships, and the core use-case flow are designed to remain consistent with the assigned problem scenario.
