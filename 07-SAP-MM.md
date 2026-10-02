# SAP MM — Detailed Practical Guide

> **File:** `07-SAP-MM.md`  
> **Purpose:** A practical SAP Materials Management (MM) guide for SAP Ariba professionals, P2P consultants, integration/support engineers, and interview preparation.
>
> **Scope:** This guide explains how SAP MM works, SAP GUI/logon concepts, organizational hierarchy, procurement and inventory processes, master data, important transactions, the relationship between SAP MM and SAP Ariba, similarities/differences, practical examples, integration flows, troubleshooting, and interview-oriented revision.
>
> **Important:** Exact screens, fields, transactions, integrations, and configuration can vary by SAP ECC/S/4HANA release, customer configuration, and enabled products.

---

# 1. What Is SAP MM?

**SAP MM (Materials Management)** is the SAP ERP/S/4HANA area responsible for processes involving:

- Procurement
- Purchasing
- Material and supplier data
- Inventory management
- Goods movements
- Stock management
- Invoice verification
- Material planning-related procurement activities
- Integration with Finance and other SAP processes

A simplified procurement lifecycle is:

```text
Business Requirement
       ↓
Purchase Requisition (PR)
       ↓
Source / Supplier
       ↓
Purchase Order (PO)
       ↓
Goods Receipt (GR)
       ↓
Invoice Receipt (IR)
       ↓
Invoice Verification
       ↓
Financial Posting / Payment Process
```

SAP MM is therefore a major ERP-side foundation for the **Procure-to-Pay (P2P)** process.

---

# 2. SAP MM in Simple Words

Imagine a company needs 100 laptops.

The business says:

> "We need 100 laptops."

SAP MM helps represent and control the procurement process:

1. A requirement is created.
2. A Purchase Requisition may be created.
3. Purchasing identifies a supplier.
4. A Purchase Order is created.
5. The supplier delivers the laptops.
6. The company records the Goods Receipt.
7. The supplier sends an invoice.
8. SAP verifies the invoice against the purchasing and receiving information.
9. Financial/accounting processes continue.

The key idea is:

> **SAP MM manages the ERP-side procurement and material/inventory lifecycle.**

---

# 3. Where SAP MM Fits in SAP

SAP MM does not operate as an isolated module.

A simplified SAP landscape is:

```text
                         SAP ERP / S/4HANA
                                |
        ------------------------------------------------
        |              |             |                |
       MM             FI            SD               PP
 Materials         Finance       Sales &          Production
 Management                      Distribution
        |
        |-------------------------------
        |              |               |
    Purchasing     Inventory       Invoice
                   Management      Verification
```

For an Ariba environment:

```text
        SAP Ariba
            |
            | Integration
            ↓
 Business Network / Managed Gateway
            |
            ↓
     SAP Integration Layer
            |
            ↓
      SAP ECC / S/4HANA
            |
            ↓
          SAP MM
            |
      ----------------
      |       |      |
      PR      PO     GR/IR
```

The exact architecture depends on the customer's SAP Ariba products, ERP release, integration approach, and configuration.

---

# 4. SAP MM Major Areas

SAP MM is commonly understood through several major functional areas.

## 4.1 Purchasing

Purchasing covers activities such as:

- Purchase requisitions
- Requests for quotation
- Supplier quotations
- Purchase orders
- Contracts
- Scheduling agreements
- Purchasing organization activities

---

## 4.2 Inventory Management

Inventory Management covers:

- Goods receipt
- Goods issue
- Stock transfer
- Transfer posting
- Physical inventory
- Stock quantities
- Material movements

---

## 4.3 Invoice Verification

Invoice verification deals with:

- Supplier invoices
- Purchase order references
- Goods receipt references
- Quantity checks
- Price checks
- Invoice blocking
- Financial integration

---

## 4.4 Material Master

The Material Master stores information about materials/products used by the organization.

Examples:

```text
Material: LAPTOP-001
Description: Business Laptop
Base Unit: EA
Material Group: IT Hardware
Plant: 1000
```

---

## 4.5 Supplier / Business Partner Data

Supplier information is required for purchasing and related processes.

In modern S/4HANA systems, supplier master functionality is centered around the **Business Partner** approach.

---

# 5. SAP MM Organizational Hierarchy

Understanding organizational structure is extremely important for both SAP MM and SAP Ariba integration.

A simplified structure:

```text
Client
  |
  +-- Company Code
        |
        +-- Plant
              |
              +-- Storage Location

Purchasing Structure:

Purchasing Organization
        |
        +-- Purchasing Group
```

These objects have different purposes.

---

# 6. Client

A **Client** is a top-level organizational/data partition in an SAP system.

Example:

```text
Client 100
```

A single SAP system can contain multiple clients depending on the landscape.

The client provides a broad boundary for system data and configuration.

---

# 7. Company Code

A **Company Code** represents an organizational unit for which a complete set of financial accounting records can be maintained.

Example:

```text
Company Code: 1000
Name: ABC India Pvt Ltd
Currency: INR
```

The company code is primarily an FI concept, but procurement transactions often have financial implications at this level.

---

# 8. Plant

A **Plant** represents a location or organizational unit where activities such as procurement, production, storage, or inventory management are performed.

Example:

```text
Company Code
    |
    +-- Plant 1100 — Bangalore
    +-- Plant 1200 — Mumbai
```

A plant can represent:

- Manufacturing location
- Warehouse
- Distribution location
- Procurement-related location

The exact meaning depends on configuration.

---

# 9. Storage Location

A **Storage Location** is a subdivision within a plant used to manage stock.

Example:

```text
Plant 1100 — Bangalore
    |
    +-- 0001 — Main Warehouse
    +-- 0002 — IT Storage
    +-- 0003 — Spare Parts
```

So:

```text
Plant = Where the organization operates

Storage Location = Where stock is managed within the plant
```

---

# 10. Purchasing Organization

The **Purchasing Organization** is responsible for procurement activities.

Example:

```text
Purchasing Org 1000
    |
    +-- India Procurement
```

It can be responsible for negotiating and purchasing materials/services for plants or company codes according to the configured purchasing model.

---

# 11. Purchasing Group

A **Purchasing Group** represents a buyer or group of buyers responsible for purchasing activities.

Example:

```text
Purchasing Group 001
Description: IT Procurement

Purchasing Group 002
Description: Raw Materials
```

A useful distinction:

```text
Purchasing Organization
        ↓
Procurement organizational responsibility

Purchasing Group
        ↓
Buyer / purchasing responsibility
```

---

# 12. Complete Organizational Example

Consider ABC Corporation.

```text
Client
  |
  +-- Company Code 1000
        |
        +-- Plant 1100 — Bangalore
        |      |
        |      +-- Storage Location 0001
        |      +-- Storage Location 0002
        |
        +-- Plant 1200 — Mumbai
               |
               +-- Storage Location 0001


Purchasing Organization 1000
        |
        +-- Purchasing Group 001 — IT
        +-- Purchasing Group 002 — Facilities
```

This structure determines where procurement and inventory transactions belong.

---

# 13. SAP MM Master Data

Master data is reusable information used by transactions.

Important examples:

- Material Master
- Supplier / Business Partner
- Purchasing Info Record
- Source List
- Service-related master data where applicable
- Classification-related data where configured

---

# 14. Material Master

The Material Master represents a material/product in SAP.

Example:

```text
Material Number: 10000001
Description: Dell Business Laptop
Material Group: IT-HARDWARE
Base UOM: EA
```

Material information can be maintained across organizational levels.

Conceptually:

```text
Material
   |
   +-- General information
   |
   +-- Plant-specific information
   |
   +-- Storage-location information
   |
   +-- Purchasing information
   |
   +-- Accounting information
```

Not every material uses every possible view or field.

---

# 15. Supplier / Business Partner

A supplier is the organization from which goods or services are procured.

Example:

```text
Supplier: ABC Technologies
Supplier ID: 3000123
Country: India
Payment Terms: ...
Currency: INR
```

In S/4HANA, the **Business Partner** model is central to customer/supplier master data.

---

# 16. Purchasing Info Record

A Purchasing Info Record stores purchasing information for a material/supplier combination.

Conceptually:

```text
Supplier
   +
Material
   ↓
Purchasing Info Record
   ↓
Purchasing-specific information
```

It can contain information such as purchasing conditions and supplier-specific material information, depending on configuration.

---

# 17. Source List

A source list can define which sources of supply are valid for a material and plant over a period.

Conceptually:

```text
Material + Plant
      ↓
Source List
      ↓
Valid Sources of Supply
```

---

# 18. Transaction Data vs Master Data

This distinction is important.

### Master Data

Reusable information:

```text
Material
Supplier
Plant
Purchasing Organization
Purchasing Group
```

### Transaction Data

Business events/documents:

```text
Purchase Requisition
Purchase Order
Goods Receipt
Invoice
```

Example:

```text
Supplier = Master Data

PO #4500012345 = Transaction Data
```

---

# 19. SAP MM Procurement Flow

A standard procurement example:

```text
Requirement
    ↓
Purchase Requisition
    ↓
Source Determination
    ↓
Purchase Order
    ↓
Supplier
    ↓
Goods Receipt
    ↓
Invoice Receipt
    ↓
Invoice Verification
    ↓
Accounting / Payment Process
```

Not every procurement process uses every document.

---

# 20. Purchase Requisition

A **Purchase Requisition (PR)** is an internal request to procure something.

Example:

> The IT department needs 20 laptops.

A PR may contain:

```text
Material / Description
Quantity
Delivery Date
Plant
Account Assignment
Requester
```

The PR is generally an internal procurement requirement.

It is different from a Purchase Order.

---

# 21. Purchase Order

A **Purchase Order (PO)** is the purchasing document used to formally order goods or services from a supplier.

Example:

```text
PO: 4500012345

Supplier: ABC Technologies

Item:
Business Laptop
Quantity: 20
Price: INR 60,000 each
Plant: 1100
Delivery Date: 15-Oct
```

The PO represents the buyer's order.

---

# 22. Purchase Order Lifecycle

A simplified lifecycle:

```text
PO Created
    ↓
PO Approved / Released
    ↓
PO Sent to Supplier
    ↓
Supplier Confirmation
    ↓
Supplier Ships
    ↓
Goods Receipt
    ↓
Invoice
```

In an Ariba-connected environment, supplier collaboration may happen through SAP Business Network.

---

# 23. Goods Receipt

When goods physically arrive, the organization records a **Goods Receipt (GR)**.

Example:

```text
PO Quantity = 20

Supplier delivers = 20

GR = 20
```

If only 15 arrive:

```text
PO = 20
GR = 15
Remaining = 5
```

The exact accounting impact depends on material valuation, configuration, and transaction details.

---

# 24. Goods Issue

A **Goods Issue (GI)** records the movement of stock out of inventory for a business purpose.

Examples:

- Material issued to production
- Material issued to a cost center
- Material scrapped
- Stock transferred through relevant movement processes

---

# 25. Movement Types

Movement types control the business meaning of material movements.

Examples commonly encountered include:

```text
101 → Goods receipt for purchase order
102 → Reversal of a 101 goods receipt
122 → Return delivery to supplier
201 → Goods issue to cost center
261 → Goods issue to production order
301 → Plant-to-plant stock transfer
311 → Storage-location transfer
```

**Important:** Movement type behavior and permitted usage depend on configuration and business process. Do not treat the list above as a universal configuration for every system.

---

# 26. Invoice Verification

After goods/services are received, the supplier invoice needs to be processed.

A common procurement control is:

```text
Purchase Order
      +
Goods Receipt
      +
Invoice
      ↓
Invoice Verification
```

This is commonly referred to as **three-way matching**.

---

# 27. Three-Way Matching

Example:

```text
PO:
100 units × ₹100
Total = ₹10,000

GR:
100 units received

Invoice:
100 units × ₹100
Total = ₹10,000
```

The documents agree.

But suppose:

```text
PO = 100 units
GR = 80 units
Invoice = 100 units
```

The invoice may require exception handling depending on tolerance and configuration.

---

# 28. Two-Way vs Three-Way Matching

### Two-way concept

```text
PO
 +
Invoice
```

The invoice is compared with purchasing information.

### Three-way concept

```text
PO
 +
Goods Receipt
 +
Invoice
```

The invoice is compared against both purchasing and receiving information.

The exact matching and blocking behavior depends on configuration and process.

---

# 29. Account Assignment

When purchasing certain goods/services, the organization may need to specify where the cost belongs.

Examples:

```text
Cost Center
Internal Order
Asset
Project / WBS
```

Example:

> Company buys a laptop for the Finance department.

The procurement document may carry an account assignment pointing to the relevant cost center.

---

# 30. SAP GUI / SAP Logon

A traditional SAP ERP/ECC/S/4HANA environment can be accessed through **SAP GUI**.

A simplified logon sequence is:

```text
SAP Logon
    ↓
Select System
    ↓
Application Server / System Connection
    ↓
Client
    ↓
User
    ↓
Password
    ↓
SAP Easy Access
```

Typical information may include:

```text
System
Client
User
Password
Language
```

The exact login screen and authentication method depend on the customer's SAP landscape.

---

# 31. SAP Logon vs SAP GUI

These terms are often confused.

### SAP Logon

The application used to maintain/select SAP system connections.

### SAP GUI

The graphical interface used to interact with SAP applications.

A simplified mental model:

```text
SAP Logon
   ↓
Choose SAP System
   ↓
SAP GUI Session
   ↓
SAP Application
```

---

# 32. SAP Easy Access

After login, users commonly reach **SAP Easy Access**.

From here, users can:

- Enter transaction codes
- Navigate menus
- Access role-based functions
- Execute reports
- Open relevant SAP transactions

---

# 33. What Is a T-Code?

A transaction code (T-code) is a shortcut used to access an SAP transaction.

Examples:

```text
ME51N → Create Purchase Requisition
ME52N → Change Purchase Requisition
ME53N → Display Purchase Requisition

ME21N → Create Purchase Order
ME22N → Change Purchase Order
ME23N → Display Purchase Order

MIGO  → Goods Movement

MIRO  → Enter Incoming Invoice
MIR4  → Display Invoice Document
```

Availability and authorization depend on the system and user's role.

---

# 34. Common SAP MM T-Codes

| Area | T-Code | Typical purpose |
|---|---|---|
| PR | ME51N | Create PR |
| PR | ME52N | Change PR |
| PR | ME53N | Display PR |
| PO | ME21N | Create PO |
| PO | ME22N | Change PO |
| PO | ME23N | Display PO |
| Goods Movement | MIGO | Goods movement |
| Invoice | MIRO | Enter invoice |
| Invoice | MIR4 | Display invoice |
| Supplier/Info | ME13 | Display info record |
| Material | MM03 | Display material |
| Material | MM01 | Create material |
| Material | MM02 | Change material |
| Stock | MMBE | Stock overview |
| Purchase Orders | ME2N | PO analysis |
| PR analysis | ME5A | PR analysis |

T-code behavior can differ by release and authorization.

---

# 35. SAP MM Example — Buying a Laptop

Business requirement:

> Finance department needs 10 laptops.

### Step 1 — Requirement

Finance requests:

```text
10 laptops
Required date: 20-Oct
Plant: Bangalore
```

### Step 2 — PR

A Purchase Requisition is created.

```text
PR = 1000012345
Quantity = 10
```

### Step 3 — Sourcing

Purchasing identifies an approved supplier.

### Step 4 — PO

```text
PO = 4500012345
Supplier = ABC Technologies
Quantity = 10
```

### Step 5 — Delivery

Supplier ships the laptops.

### Step 6 — GR

Warehouse receives 10 laptops.

```text
GR = 10
```

### Step 7 — Invoice

Supplier sends invoice.

### Step 8 — Verification

SAP compares the relevant PO, receipt, and invoice information.

---

# 36. SAP MM and SAP Ariba

This is particularly important for an SAP Ariba consultant.

A simplified relationship is:

```text
SAP Ariba
   |
   | Procurement / Sourcing / Collaboration
   ↓
SAP Business Network
   |
   | Integration
   ↓
Managed Gateway / Integration Layer
   |
   ↓
SAP ECC / S/4HANA
   |
   ↓
SAP MM
```

The exact integration architecture varies by customer.

---

# 37. What SAP Ariba Does vs What SAP MM Does

A useful conceptual distinction:

### SAP Ariba

Often provides cloud-based capabilities around:

- Sourcing
- Supplier management
- Procurement
- Buying
- Guided Buying
- Contracts
- Supplier collaboration
- Business Network
- Procurement-related user experience

### SAP MM

Provides ERP-side capabilities around:

- Purchasing
- Material management
- Inventory
- Goods movements
- Invoice verification
- ERP procurement processing
- Financial/accounting integration

There is overlap in procurement processes, but they are not simply two names for the same product.

---

# 38. SAP Ariba vs SAP MM — Simple Comparison

| Area | SAP Ariba | SAP MM |
|---|---|---|
| Primary orientation | Cloud procurement / spend processes | ERP materials/procurement |
| Sourcing | Strong capability | Can support procurement source processes, depending on scope |
| Supplier collaboration | Strong through Business Network | ERP-side supplier processing |
| Guided Buying | Yes, in Ariba Buying solutions | Not the same product capability |
| Inventory | Not the primary ERP inventory system | Core capability |
| Goods Receipt | Can participate in procurement workflows | ERP-side material receipt |
| Material stock | Not the primary stock ledger | Core capability |
| Invoice processing | Ariba invoice capabilities | ERP invoice verification |
| ERP accounting | Integrates with ERP | Native ERP integration |
| Supplier network | Business Network | ERP supplier master/business partner |
| User experience | Cloud/web oriented | SAP GUI/Fiori depending on system |
| Integration | APIs/cXML/integration services/etc. | ERP interfaces, IDocs, APIs, services, etc. |

---

# 39. SAP Ariba and SAP MM Similarities

Both can participate in procurement processes involving:

- Suppliers
- Purchase requisitions
- Purchase orders
- Approvals
- Catalogs
- Procurement policies
- Invoices
- Procurement data
- Supplier/material information

Both can therefore appear in the same P2P landscape.

---

# 40. Key Difference: Procurement Front End vs ERP Back End

A simplified enterprise architecture can look like:

```text
                USER / BUYER
                     |
                     ↓
              SAP Ariba Buying
                     |
                     ↓
           Procurement Processing
                     |
                     ↓
            Integration Layer
                     |
                     ↓
              SAP ECC / S/4HANA
                     |
                     ↓
                 SAP MM
                     |
          -----------------------
          |          |          |
       Inventory   Goods      Accounting
                  Movement
```

Do not interpret this as saying every Ariba customer uses this exact architecture. It is a conceptual model.

---

# 41. Ariba P2O and SAP MM P2P

There can be significant process overlap.

### Ariba-oriented view

```text
Requisition
    ↓
Approval
    ↓
Purchase Order
    ↓
Business Network
    ↓
Supplier
```

### ERP/MM-oriented view

```text
PR
 ↓
Purchasing
 ↓
PO
 ↓
Goods Receipt
 ↓
Invoice
 ↓
Accounting
```

In an integrated landscape, these become one larger end-to-end process.

---

# 42. Example: Ariba Buying + SAP MM

Suppose a company uses:

```text
SAP Ariba Buying
SAP Business Network
SAP S/4HANA
SAP MM
```

A user creates a shopping cart in Ariba.

```text
User
 ↓
Ariba Shopping Cart
 ↓
Approval
 ↓
PR / procurement document
 ↓
Integration
 ↓
S/4HANA
 ↓
Purchasing / PO
 ↓
Supplier
```

Supplier collaboration can occur through Business Network.

After delivery:

```text
Supplier
 ↓
Business Network
 ↓
ERP
 ↓
Goods Receipt
 ↓
Invoice
 ↓
Invoice Verification
```

The exact document mapping depends on the implementation.

---

# 43. Example: Ariba P2O Support Engineer

Suppose a customer reports:

> "The PO was created in Ariba but the supplier has not received it."

Do not immediately conclude:

> "CIG is broken."

Instead trace the transaction.

```text
Ariba
  ↓
Business Network
  ↓
Managed Gateway / Integration
  ↓
ERP
  ↓
Supplier
```

Ask:

1. Was the PO created successfully?
2. Was the PO approved?
3. Was the expected output generated?
4. Was the integration message created?
5. Did the message reach the integration layer?
6. Was the payload valid?
7. Was routing successful?
8. Did Business Network receive the document?
9. Is the supplier relationship enabled?
10. Was the document delivered to the supplier?

This is the same troubleshooting mindset used in production integration support.

---

# 44. Example: PO Created but Not in ERP

Scenario:

```text
Ariba
  ↓
PO created
  ↓
Integration
  X
ERP does not show PO
```

Possible layers:

```text
Ariba document generation
        ↓
Integration message
        ↓
Mapping
        ↓
Authentication
        ↓
Network
        ↓
ERP endpoint
        ↓
ERP processing
```

Possible root causes include:

- Mapping issue
- Invalid payload
- Authentication issue
- Endpoint problem
- Master-data mismatch
- ERP validation failure
- Interface processing failure

The correct root cause must be established from evidence.

---

# 45. Example: Supplier Not Available

Suppose a buyer searches for a supplier in an Ariba process.

Possible areas to investigate:

```text
Supplier Master
      ↓
Supplier relationship
      ↓
Supplier status
      ↓
Qualification
      ↓
Purchasing organization
      ↓
Ariba/ERP master-data integration
```

The exact path depends on which Ariba solution and supplier process is being used.

---

# 46. Master Data Relationship

An integrated procurement environment may have:

```text
SAP ERP / S4
    |
    +-- Material
    +-- Supplier / Business Partner
    +-- Plant
    +-- Company Code
    +-- Purchasing Organization
    +-- Purchasing Group
    +-- Cost Center
    |
    ↓
Integration
    |
    ↓
SAP Ariba
```

If master data is incorrect, transactional processing can fail even when the integration itself is technically functioning.

---

# 47. Why MM Knowledge Matters for an Ariba Consultant

If you support SAP Ariba P2P, understanding MM helps you understand the ERP side.

For example:

```text
Ariba PR
   ↓
ERP PR

Ariba PO
   ↓
ERP PO

ERP Goods Receipt
   ↓
Procurement lifecycle

ERP Invoice
   ↓
Invoice verification
```

Without MM knowledge, it is easy to treat ERP behavior as a black box.

With MM knowledge, you can ask:

> Which ERP document was created?

> Which organizational unit owns it?

> Which master data does it reference?

> What happened to the goods receipt?

> What caused the invoice block?

---

# 48. SAP Ariba ↔ SAP MM Data Categories

Typical integration areas can include:

### Master Data

```text
Supplier
Material
Plant
Company Code
Purchasing Organization
Purchasing Group
Account-related data
```

### Transaction Data

```text
Purchase Requisition
Purchase Order
Order Confirmation
Advance Shipping Notice
Goods Receipt
Invoice
```

The actual objects and direction depend on the solution and integration design.

---

# 49. SAP Ariba and SAP MM — Where Each Is Strong

Think in terms of responsibilities rather than declaring one system universally "better."

### Ariba is commonly used for:

```text
Supplier collaboration
Sourcing
Cloud procurement experience
Guided Buying
Spend management
Business Network
```

### SAP MM is commonly used for:

```text
ERP procurement
Inventory
Material movements
Goods receipt
Stock
ERP purchasing
Invoice verification
ERP accounting integration
```

A customer's architecture may distribute responsibilities differently.

---

# 50. SAP MM vs SAP Ariba — Important Interview Answer

**Question: What is the difference between SAP MM and SAP Ariba?**

A strong answer:

> SAP MM is an ERP-side materials management and procurement capability used for purchasing, inventory management, goods movements and invoice verification. SAP Ariba is a cloud-based spend and procurement ecosystem that provides capabilities such as sourcing, buying, supplier management and supplier collaboration through Business Network. In an integrated landscape, Ariba can handle cloud procurement and supplier-facing processes while SAP MM/S/4HANA handles ERP-side procurement, inventory and financial integration. The exact split depends on the customer's solution architecture.

---

# 51. SAP MM and S/4HANA

SAP S/4HANA is the ERP platform in which modern SAP MM functionality is delivered.

A simplified conceptual relationship:

```text
SAP S/4HANA
    |
    +-- MM
    +-- FI
    +-- SD
    +-- PP
    +-- Other business areas
```

S/4HANA does not mean MM disappears.

Instead, MM capabilities are part of the modern ERP platform, with changes in data models, user interfaces, and business processes compared with older ECC implementations.

---

# 52. ECC vs S/4HANA — MM Perspective

### SAP ECC

Traditional SAP ERP environment.

### SAP S/4HANA

Modern SAP ERP platform based on SAP HANA.

From an Ariba integration/support perspective, you should understand that:

```text
Ariba
  ↓
Integration
  ↓
ECC
```

and

```text
Ariba
  ↓
Integration
  ↓
S/4HANA
```

can have different implementation details.

Do not assume a transaction, table, API, or integration behavior is identical across releases.

---

# 53. SAP MM Technical Troubleshooting Model

When a procurement issue occurs, classify it first.

```text
Business Requirement
       ↓
Master Data
       ↓
Configuration
       ↓
Transaction
       ↓
Integration
       ↓
ERP Processing
       ↓
Accounting / Inventory
```

Ask:

> Where did the process stop?

Then ask:

> Why did it stop?

---

# 54. Troubleshooting Example — PO Failure

Problem:

> PO is not reaching ERP.

Trace:

```text
1. Check Ariba PO
2. Check document status
3. Check integration message
4. Inspect payload
5. Check routing
6. Check authentication
7. Check ERP endpoint
8. Check ERP application processing
9. Check logs
```

Possible SAP-side tools can include:

```text
SLG1
WE02 / WE05
BD87
SRT_MONI
SM58
SM59
SM37
ST22
SM21
```

The appropriate transaction depends on the interface and failure layer.

---

# 55. Important SAP MM Support Transactions

## Purchasing

```text
ME51N
ME52N
ME53N

ME21N
ME22N
ME23N
```

## Inventory

```text
MIGO
MMBE
```

## Invoice

```text
MIRO
MIR4
```

## Material

```text
MM01
MM02
MM03
```

## Analysis

```text
ME2N
ME5A
```

---

# 56. SAP MM Logs and Integration Support

For integration problems, the MM consultant may work with technical/integration teams.

A simplified troubleshooting chain:

```text
Business User
      ↓
Ariba Support
      ↓
Integration Support
      ↓
SAP MM / Functional Team
      ↓
ABAP / Basis / Middleware
```

Not every incident follows this exact ownership model.

The important skill is to identify the correct layer and provide evidence.

---

# 57. Example — Invoice Block

Scenario:

```text
PO = 100 units
GR = 80 units
Invoice = 100 units
```

The invoice may be blocked depending on configuration/tolerance.

Investigation:

```text
PO
 ↓
GR
 ↓
Invoice
 ↓
Matching result
 ↓
Exception / Block
```

A support engineer should determine whether the discrepancy is:

- Quantity
- Price
- Tax
- Supplier
- PO data
- GR data
- Configuration/tolerance
- Master data

---

# 58. Example — Wrong Plant

Problem:

> User expected the material to be available in Bangalore, but procurement was created for another plant.

Trace:

```text
Requirement
 ↓
PR
 ↓
Plant
 ↓
Source determination
 ↓
PO
 ↓
Goods receipt
```

Potential causes:

- Incorrect requester input
- Incorrect master data
- Incorrect organizational assignment
- Configuration
- Integration mapping

---

# 59. Example — Material Not Found

If a user cannot find a material, investigate:

```text
Material number
Material status
Plant extension
Purchasing data
Authorization
Search criteria
Master-data replication
```

Do not immediately classify it as an Ariba defect.

---

# 60. Example — Supplier PO Not Received

End-to-end trace:

```text
SAP MM PO
     ↓
Integration
     ↓
Business Network
     ↓
Supplier Relationship
     ↓
Supplier Account
     ↓
Supplier Inbox / Transaction
```

Questions:

1. Does the PO exist in ERP?
2. Was output generated?
3. Did integration create a message?
4. Was payload accepted?
5. Did Business Network receive it?
6. Was the supplier relationship active?
7. Is the supplier account correctly connected?
8. Was the document delivered?

---

# 61. SAP MM and SAP Ariba Process Mapping

| Business Activity | SAP Ariba Side | SAP MM / ERP Side |
|---|---|---|
| Shopping | Buying / Guided Buying | ERP procurement processing where integrated |
| Requisition | Ariba requisition | ERP PR where integrated |
| Approval | Ariba approval | ERP release strategy/workflow where applicable |
| Supplier sourcing | Ariba Sourcing | ERP purchasing/source data where applicable |
| PO | Ariba / integrated procurement | MM purchasing document |
| Supplier collaboration | Business Network | ERP receives/sends relevant documents |
| Goods receipt | May be represented in procurement flow | MM inventory transaction |
| Invoice | Ariba invoicing capabilities | ERP invoice verification |
| Stock | Not primary ERP stock ledger | MM Inventory Management |
| Accounting | Integrates with ERP | FI integration |

---

# 62. Ariba P2O vs SAP MM P2P

## Ariba P2O

```text
Requisition
   ↓
Approval
   ↓
Purchase Order
   ↓
Supplier Collaboration
   ↓
Receipt / Invoice processes
```

## SAP MM P2P

```text
Requirement
   ↓
PR
   ↓
PO
   ↓
GR
   ↓
Invoice Verification
   ↓
Accounting
```

## Integrated view

```text
             SAP Ariba
                 |
        Procurement Experience
                 |
                 ↓
       Integration Platform
                 |
                 ↓
          SAP S/4HANA
                 |
             SAP MM
                 |
        -------------------
        |        |        |
       PO       GR       Invoice
```

---

# 63. SAP MM Practical Use Cases

### Use Case 1 — Office Supplies

```text
Requirement
 ↓
PR
 ↓
PO
 ↓
Delivery
 ↓
GR
 ↓
Invoice
```

### Use Case 2 — Raw Material

```text
Production requirement
 ↓
Procurement
 ↓
PO
 ↓
Material receipt
 ↓
Inventory
 ↓
Production consumption
```

### Use Case 3 — IT Hardware

```text
Employee/department requirement
 ↓
Procurement
 ↓
Supplier
 ↓
PO
 ↓
GR
 ↓
Asset/cost assignment
 ↓
Invoice
```

### Use Case 4 — Service Procurement

```text
Service requirement
 ↓
Purchase Order
 ↓
Service confirmation / receipt
 ↓
Invoice
```

The exact document model depends on configuration.

---

# 64. SAP MM in a Real Support Day

A practical support engineer may receive tickets such as:

```text
"PO is not created"
"PO is not reaching supplier"
"Material is not visible"
"Supplier cannot be selected"
"GR cannot be posted"
"Invoice is blocked"
"Wrong price on PO"
"Wrong plant"
"Wrong supplier"
"PO stuck"
"Invoice mismatch"
```

A structured investigation is:

```text
Understand business scenario
        ↓
Identify document
        ↓
Identify document number
        ↓
Check status
        ↓
Check master data
        ↓
Check configuration
        ↓
Check integration
        ↓
Check ERP processing
        ↓
Identify root cause
        ↓
Fix
        ↓
Reprocess if appropriate
        ↓
Validate
```

---

# 65. Document Numbers Matter

When supporting SAP MM, collect identifiers.

Examples:

```text
PR Number
PO Number
Material Number
Supplier Number
GR Document
Invoice Document
Accounting Document
Integration Message ID
```

A vague ticket:

> "My PO is not working."

is difficult to troubleshoot.

A useful ticket:

> "PO 4500012345 was created at 14:32 IST for supplier 3000123 and has not reached Business Network."

is much more actionable.

---

# 66. Production Support Mindset

Never troubleshoot only from the symptom.

Example:

```text
Symptom:
Supplier did not receive PO.

Possible root causes:
- PO not approved
- Output not generated
- Mapping error
- Supplier relationship issue
- Network issue
- Payload validation error
- ERP/interface error
```

Therefore:

> **Symptom ≠ Root Cause**

This is one of the most important principles in Ariba/MM support.

---

# 67. Configuration vs Master Data vs Transaction

### Configuration

Defines how the system behaves.

### Master Data

Defines reusable business objects.

### Transaction

Represents a specific business event.

Example:

```text
Configuration:
Tolerance rule

Master Data:
Supplier ABC

Transaction:
PO 4500012345
```

A defect can originate in any of these layers.

---

# 68. SAP MM + Ariba Interview Scenario

### Question

> A user creates a requisition in Ariba but the corresponding ERP document is not available. How would you troubleshoot?

### Answer Framework

```text
1. Confirm the Ariba document exists.
2. Check document status.
3. Identify whether an ERP document was expected.
4. Check integration message/log.
5. Inspect payload and mapping.
6. Check master-data references.
7. Check ERP endpoint/interface.
8. Check ERP application processing.
9. Identify exact failure layer.
10. Correct the root cause.
11. Reprocess only after checking duplicate-document risk.
12. Validate the end-to-end result.
```

This is a stronger answer than simply saying:

> "I will check CIG."

---

# 69. SAP MM Interview Questions

## Q1. What is SAP MM?

SAP MM is the SAP materials management area covering procurement, purchasing, inventory management, goods movements, and invoice verification.

---

## Q2. What is the difference between PR and PO?

```text
PR = Internal requirement/request to procure

PO = Formal purchasing document sent/issued to supplier
```

---

## Q3. What is Goods Receipt?

Goods Receipt records the receipt of goods against a procurement document where applicable.

---

## Q4. What is Invoice Verification?

It is the process of checking supplier invoices against relevant purchasing and receiving information and posting/processing the invoice according to configuration.

---

## Q5. What is a plant?

A plant is an organizational unit representing a location or operational unit where procurement, inventory, production, or related activities occur.

---

## Q6. What is a storage location?

A storage location is a subdivision of a plant used to manage stock.

---

## Q7. What is a purchasing organization?

It is an organizational unit responsible for purchasing activities.

---

## Q8. What is a purchasing group?

It represents an individual buyer or group of buyers responsible for procurement activities.

---

## Q9. What is a movement type?

A movement type identifies and controls the business meaning of a goods movement.

---

## Q10. What is three-way matching?

It compares relevant:

```text
PO
+
Goods Receipt
+
Invoice
```

to validate the invoice before processing according to configured controls.

---

# 70. Ariba + MM Interview Questions

## Q11. How does SAP Ariba integrate with SAP MM?

A strong answer:

> SAP Ariba can integrate with SAP ECC or S/4HANA so that procurement and supplier-facing processes in Ariba can exchange master and transactional data with the ERP. The integration can involve Business Network, managed gateway/integration services, APIs, cXML, IDocs, web services, and other interfaces depending on the customer's architecture.

---

## Q12. Is SAP Ariba a replacement for SAP MM?

Not simply.

They provide different capabilities and can work together.

```text
Ariba
→ Cloud procurement / sourcing / supplier collaboration

SAP MM
→ ERP procurement / inventory / goods movement / invoice verification
```

---

## Q13. Why should an Ariba consultant know MM?

Because many Ariba procurement transactions ultimately interact with ERP procurement, inventory, and financial processes.

---

## Q14. What happens after a PO reaches ERP?

Depending on the process:

```text
Supplier receives PO
      ↓
Supplier confirms
      ↓
Supplier ships
      ↓
Goods Receipt
      ↓
Invoice
      ↓
Invoice Verification
```

---

# 71. Quick T-Code Revision

```text
PR:
ME51N
ME52N
ME53N

PO:
ME21N
ME22N
ME23N

Material:
MM01
MM02
MM03

Goods Movement:
MIGO

Invoice:
MIRO
MIR4

Stock:
MMBE

PO Analysis:
ME2N

PR Analysis:
ME5A
```

---

# 72. Quick Organizational Revision

Remember:

```text
Client
  ↓
Company Code
  ↓
Plant
  ↓
Storage Location
```

And separately:

```text
Purchasing Organization
  ↓
Purchasing Group
```

Do not describe Purchasing Group as a child organizational level of Purchasing Organization in the same structural sense as Storage Location is under Plant. They represent different organizational concepts.

---

# 73. Quick Procurement Revision

```text
Requirement
 ↓
PR
 ↓
Source
 ↓
PO
 ↓
Supplier
 ↓
GR
 ↓
Invoice
 ↓
Verification
 ↓
Accounting
```

---

# 74. Quick Ariba + MM Revision

```text
SAP Ariba
    ↓
Procurement / Sourcing / Supplier Collaboration
    ↓
Business Network
    ↓
Integration Layer
    ↓
SAP ECC / S4HANA
    ↓
SAP MM
    ↓
PO / GR / Inventory / Invoice Verification
```

---

# 75. Mental Model

If you remember only one thing:

```text
SAP Ariba
= Cloud procurement + sourcing + supplier collaboration

SAP Business Network
= Supplier/business document collaboration layer

Integration
= Moves/transforms/routes data between systems

SAP MM
= ERP procurement + materials + inventory + goods movement

SAP FI
= Financial/accounting side
```

And the complete business process can be understood as:

```text
Business Need
     ↓
Ariba / Procurement Experience
     ↓
Requisition
     ↓
Approval
     ↓
Purchasing
     ↓
PO
     ↓
Supplier / Business Network
     ↓
Delivery
     ↓
Goods Receipt
     ↓
Invoice
     ↓
Invoice Verification
     ↓
Accounting / Payment
```

---

# 76. Practical Checklist for an Ariba Consultant

Before saying you understand SAP MM, make sure you can explain:

- [ ] SAP MM purpose
- [ ] SAP GUI and SAP Logon
- [ ] SAP Easy Access
- [ ] T-codes
- [ ] Client
- [ ] Company Code
- [ ] Plant
- [ ] Storage Location
- [ ] Purchasing Organization
- [ ] Purchasing Group
- [ ] Material Master
- [ ] Supplier/Business Partner
- [ ] Purchasing Info Record
- [ ] Source List
- [ ] PR
- [ ] PO
- [ ] GR
- [ ] GI
- [ ] Movement Types
- [ ] Invoice Verification
- [ ] Two-way/three-way matching
- [ ] Account Assignment
- [ ] Inventory Management
- [ ] Ariba P2O
- [ ] Business Network
- [ ] Ariba ↔ ERP integration
- [ ] Master-data integration
- [ ] Transaction-data integration
- [ ] Troubleshooting methodology
- [ ] ECC vs S/4HANA basics

---

# 77. Final Takeaway

SAP MM should not be learned as a collection of T-codes.

The useful mental model is:

```text
ORGANIZATION
     ↓
MASTER DATA
     ↓
PROCUREMENT
     ↓
TRANSACTIONS
     ↓
GOODS MOVEMENT
     ↓
INVOICE
     ↓
ACCOUNTING
```

For an SAP Ariba consultant, extend that model:

```text
                SAP ARIBA
                    ↓
        Procurement / Sourcing
                    ↓
           Business Network
                    ↓
              Integration
                    ↓
             SAP ECC / S4
                    ↓
                SAP MM
                    ↓
          -------------------
          |        |        |
         PO       GR      Invoice
                   |
                Inventory
```

The goal is not to memorize where a button is.

The goal is to understand:

> **What business event happened, which SAP document represents it, which organizational unit owns it, which master data it uses, where the document moves next, and what evidence can prove where a failure occurred.**

That mindset is what connects SAP MM knowledge with real SAP Ariba P2P and production-support work.
