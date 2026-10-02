# SAP Ariba S2C — Source-to-Contract Complete Guide

> A practical end-to-end reference for SAP Ariba Source-to-Contract (S2C), covering upstream procurement concepts, Supplier Lifecycle and Performance (SLP), supplier onboarding, qualification, sourcing projects, RFIs/RFPs, bidding, auctions, evaluation, award, and the transition toward contracting and downstream procurement.

**Audience:** SAP Ariba learners, support engineers, consultants, functional analysts, implementation teams, sourcing professionals, and interview candidates.

**Scope note:** SAP Ariba capabilities, terminology, user interfaces, and available features can vary by solution, architecture, subscription, configuration, and release. Examples in this guide are intentionally simplified and fictional. Always validate implementation-specific behavior against the applicable SAP documentation.

---

## 1. What is S2C?

**Source-to-Contract (S2C)** covers the strategic procurement lifecycle from identifying a sourcing requirement through supplier discovery, supplier qualification, competitive sourcing, evaluation, award, and contract creation/management.

A simplified S2C lifecycle is:

```text
Business Need
     ↓
Category / Spend Analysis
     ↓
Sourcing Strategy
     ↓
Supplier Discovery
     ↓
Supplier Registration / Onboarding
     ↓
Supplier Qualification
     ↓
Sourcing Project
     ↓
RFI / RFP / Auction
     ↓
Bid Collection
     ↓
Evaluation & Scoring
     ↓
Negotiation / Optimization
     ↓
Award
     ↓
Contract
     ↓
Contract Compliance / Downstream Buying
```

The exact lifecycle is not always linear. An organization may already know its suppliers, skip an RFI, run an RFP followed by an auction, or use an existing qualified supplier without a new onboarding cycle.

### S2C vs P2O

| Area | S2C | P2O |
|---|---|---|
| Primary purpose | Find, evaluate, select and contract with suppliers | Buy goods/services from approved suppliers |
| Main question | "Who should we buy from and under what commercial terms?" | "How do we execute the purchase?" |
| Typical activities | Sourcing, qualification, bidding, award, contracting | Requisition, catalog, PO, receipt, invoice |
| Typical outputs | Supplier award, negotiated terms, contract | Purchase order, receipt, invoice |
| Main users | Sourcing/category/procurement teams | Requesters, buyers, AP, procurement operations |

---

# 2. Core S2C Concepts

## 2.1 Category Management

A **category** groups related goods or services that are managed together from a procurement perspective.

Examples:

```text
IT
├── Laptops
├── Servers
├── Software
└── IT Services

Facilities
├── Security
├── Cleaning
├── Maintenance
└── Office Supplies
```

Category management can influence:

- sourcing strategy
- supplier selection
- event participants
- qualification requirements
- preferred supplier decisions
- contract strategy
- spend analysis

---

## 2.2 Commodity

In SAP Ariba, a commodity/category classification can be used to describe what a supplier provides or what a sourcing item represents.

Example:

```text
Commodity: IT Hardware
    ├── Laptops
    ├── Monitors
    └── Networking Equipment
```

Supplier qualification and preferred supplier processes can be associated with combinations of **commodity, region, and department**, depending on configuration.

---

## 2.3 Supplier

A supplier is the external organization that provides goods or services.

A supplier can have:

- organization information
- contacts/users
- addresses
- tax information
- banking information
- certificates
- qualifications
- preferred status
- performance information
- transaction/network relationships

Do not treat "supplier exists" and "supplier is qualified for a particular category" as the same thing.

---

# 3. SAP Ariba Supplier Lifecycle and Performance (SLP)

SLP is used to manage supplier information and lifecycle processes.

A simplified lifecycle is:

```text
Supplier Need
     ↓
Supplier Request / Discovery
     ↓
Registration
     ↓
Qualification
     ↓
Preferred Supplier
     ↓
Ongoing Management
     ↓
Requalification / Disqualification
```

The actual lifecycle depends on the organization's configuration.

SAP documentation describes supplier lifecycle management as including activities such as adding suppliers, collecting and maintaining supplier profile information, inviting suppliers to register, qualifying suppliers, making suppliers preferred, and disqualifying suppliers.

---

# 4. Supplier Request

A supplier request is commonly the starting point when an organization needs to introduce a supplier into its managed supplier population.

Example:

```text
Business asks:
"We need a new cybersecurity consulting supplier."

        ↓

Supplier Request

        ↓

Internal review

        ↓

Registration
```

Typical questions:

- Why is the supplier needed?
- Which category does the supplier belong to?
- Which region/country?
- Which department owns the relationship?
- Is the supplier already known?
- Is there an existing supplier that could meet the requirement?

---

# 5. Supplier Registration / Onboarding

Registration collects detailed supplier information.

Typical registration information may include:

### Organization

- Legal name
- Trading name
- Address
- Country
- Organization type
- Company identifiers

### Contacts

- Main contact
- Sales contact
- Finance contact
- Legal contact

### Financial

- Bank information
- Payment-related information
- Currency
- Tax information

### Compliance

- Certifications
- Diversity information
- Insurance
- Regulatory information
- Compliance questionnaires

The exact fields are implementation-specific.

SAP's current Supplier Registration Management documentation describes registration as a process where a registration manager starts a registration, suppliers provide information through questionnaires, and approvers review and approve or deny the registration.

---

# 6. Supplier Self-Registration

A supplier can be invited to provide its own information.

Simplified flow:

```text
Buyer
  ↓
Invites Supplier
  ↓
Supplier receives invitation
  ↓
Supplier completes questionnaire
  ↓
Supplier submits
  ↓
Internal review
  ↓
Approve / Deny / Return
```

### Example

A company wants to onboard:

> "ABC Cybersecurity Services Pvt. Ltd."

The supplier receives a registration questionnaire containing:

```text
Company Information
Tax Information
Bank Information
Certifications
Contact Information
Category Information
Compliance Questions
```

The buyer reviews the submitted information before allowing the supplier to progress.

---

# 7. Supplier Registration vs Supplier Qualification

This distinction is extremely important in interviews.

### Registration asks:

> "Who is this supplier and can we establish their basic profile?"

### Qualification asks:

> "Is this supplier suitable for a particular business requirement/category/region?"

Example:

```text
ABC Ltd.
   ↓
Registered
   ↓
Can provide IT Services?
   ↓
Qualification assessment
   ↓
Qualified for:
IT Services + India + IT Department
```

A supplier can be registered without being qualified for every commodity or region.

---

# 8. Supplier Qualification

Qualification evaluates whether a supplier is suitable for a particular business context.

SAP documentation describes qualification around combinations such as:

```text
Commodity
+
Region
+
Department
```

Example:

```text
Supplier: ABC Ltd.

Commodity: Cybersecurity Services
Region: India
Department: Information Security

Qualification:
QUALIFIED
```

The same supplier might not be qualified for:

```text
Commodity: Construction
Region: Germany
Department: Facilities
```

unless the organization has separately qualified them for that combination.

---

# 9. Qualification Questionnaire

A qualification questionnaire can ask suppliers to provide information such as:

```text
1. Do you hold ISO 27001 certification?
2. How many years have you provided cybersecurity services?
3. Do you have operations in India?
4. Provide relevant certifications.
5. Provide customer references.
6. Confirm regulatory compliance.
7. Provide financial information.
```

Questions may be:

- required
- optional
- scored
- informational
- conditional

A qualification decision can involve internal reviewers and approval workflows.

---

# 10. Qualification Status

Do not memorize one universal status flow without checking the implementation.

SAP Ariba can maintain qualification information at supplier level and for individual qualifications. A supplier can have multiple qualifications for different commodity/region/department combinations.

Conceptually:

```text
Qualification Request
       ↓
Questionnaire
       ↓
Supplier Submission
       ↓
Internal Review
       ↓
Approval
       ↓
Qualified
```

Possible outcomes include:

```text
Qualified
Not Qualified / Disqualified
Pending
Requalification Required
```

The exact statuses and process depend on configuration and the solution architecture.

---

# 11. Requalification

Supplier qualification is not necessarily a one-time activity.

A supplier may need requalification when:

- certification expires
- risk changes
- business scope changes
- supplier information changes
- regulatory requirements change
- a periodic review is required

Example:

```text
ABC Ltd.
   ↓
Qualified in 2026
   ↓
ISO certificate expires
   ↓
Requalification
   ↓
New evidence/questionnaire
   ↓
Review
   ↓
Qualified / Not Qualified
```

---

# 12. Disqualification

A supplier may become unsuitable for a category or process.

Examples:

- expired certification
- failed compliance requirement
- unacceptable risk
- poor performance
- regulatory issue
- business relationship terminated

Disqualification should be treated as a governed business process rather than simply deleting the supplier.

---

# 13. Preferred Supplier

Preferred supplier status answers a different question:

> "Among qualified suppliers, which supplier(s) does the organization prefer for a particular business context?"

SAP documentation describes preferred category statuses for combinations of commodity, region, and department.

Conceptually:

```text
Registered
    ↓
Qualified
    ↓
Preferred
```

But **preferred does not simply mean "best supplier in the world."**

It is a business designation based on organizational policy and context.

---

# 14. Supplier 360 / Supplier Profile

Supplier information can be viewed through a consolidated supplier profile.

Depending on the solution and UI, supplier information can include areas such as:

- common information
- registration
- qualification
- preferred status
- questionnaires
- processes
- activity/history
- documents
- contacts

The supplier profile should be treated as the central view of supplier lifecycle information.

---

# 15. Supplier Lifecycle Example

### Business requirement

A company needs a new cloud security supplier.

```text
Requirement
    ↓
Supplier Request
    ↓
Registration
    ↓
Supplier provides company/tax/compliance data
    ↓
Internal approval
    ↓
Qualification
    ↓
Security questionnaire
    ↓
Review
    ↓
Qualified
    ↓
Sourcing Event
```

This shows why SLP and Sourcing are related but different.

**SLP manages supplier readiness and lifecycle.**

**Sourcing manages competitive commercial selection.**

---

# 16. Strategic Sourcing

Strategic sourcing is the process of identifying and selecting suppliers based on business, commercial, technical, quality, risk, and other criteria.

A typical sourcing lifecycle:

```text
Spend / Requirement Analysis
          ↓
Sourcing Strategy
          ↓
Supplier Identification
          ↓
Event Design
          ↓
RFI / RFP / Auction
          ↓
Supplier Responses
          ↓
Evaluation
          ↓
Negotiation
          ↓
Award
          ↓
Contract
```

---

# 17. Sourcing Request

In organizations using sourcing requests, a business user can initiate a sourcing requirement.

Example:

```text
Marketing needs:
₹5 crore annual media services

        ↓

Sourcing Request

        ↓

Category/Sourcing review

        ↓

Sourcing Project/Event
```

SAP documentation describes approved sourcing requests being used to create sourcing projects or events.

---

# 18. Sourcing Project

A sourcing project provides the framework around a sourcing initiative.

A project may contain:

- team
- tasks
- documents
- sourcing events
- approvals
- timelines
- award activities

Example:

```text
Project:
"2027 Enterprise Laptop Sourcing"

Timeline:
1 Jan → 30 Apr

Tasks:
Business Requirement
Market Research
RFI
RFP
Evaluation
Negotiation
Award
Contract
```

---

# 19. Sourcing Event

An event is the mechanism used to collect information or bids from suppliers.

Common event types include:

### RFI — Request for Information

Used to gather information.

### RFP — Request for Proposal

Used to obtain proposals, including commercial and non-commercial information.

### Auction

Used for competitive real-time bidding.

SAP's current event management documentation identifies RFI, RFP, and auctions as core event types.

---

# 20. RFI — Request for Information

An RFI is generally non-competitive.

Purpose:

```text
"What can the market provide?"
```

Example:

A company needs:

> Cloud infrastructure services.

RFI questions:

```text
Do you support AWS?
Do you support Azure?
How many enterprise customers do you have?
What certifications do you hold?
What regions do you operate in?
What SLA levels can you support?
```

An RFI can help narrow the supplier population before a commercial event.

---

# 21. RFI Example

```text
Company:
Global Manufacturing Ltd.

Requirement:
Cloud Managed Services

RFI Participants:
Supplier A
Supplier B
Supplier C
Supplier D
Supplier E

RFI Results:

A → Meets requirements
B → Meets requirements
C → Does not meet India coverage
D → Meets requirements
E → Does not meet security requirement

Shortlist:
A, B, D
```

The shortlisted suppliers can then participate in an RFP or auction.

---

# 22. RFP — Request for Proposal

An RFP asks suppliers to propose a solution against defined requirements.

An RFP can contain:

- technical questions
- commercial questions
- pricing
- delivery information
- service levels
- implementation approach
- assumptions
- documents
- certifications
- terms

The RFP is often more structured and commercially significant than an RFI.

---

# 23. RFP Example

Requirement:

```text
5,000 laptops
3-year support
Delivery across India
```

Supplier response:

```text
Supplier A
Hardware: ₹72,000/unit
Support: ₹8,000/unit/year
Delivery: 4 weeks

Supplier B
Hardware: ₹69,000/unit
Support: ₹11,000/unit/year
Delivery: 6 weeks
```

The buyer should not automatically select the lowest price.

Evaluation can include:

```text
Price
Quality
Delivery
Technical compliance
Warranty
Service
Risk
Sustainability
```

---

# 24. Sourcing Event Structure

A sourcing event can contain multiple sections.

Conceptually:

```text
Event
│
├── Introduction
├── Prerequisites
├── General Questions
├── Technical Requirements
├── Commercial Questions
├── Pricing
├── Attachments
└── Terms / Conditions
```

The actual sections depend on the event template and configuration.

---

# 25. Event Prerequisites

Prerequisites can control whether a supplier can participate.

Examples:

```text
Accept bidder agreement
        ↓
Answer mandatory prerequisite questions
        ↓
Provide required documents
        ↓
Access event
```

This is useful when suppliers must agree to terms or demonstrate minimum eligibility before bidding.

---

# 26. Supplier Invitation

A buyer selects suppliers to participate.

Potential sources include:

- existing suppliers
- qualified suppliers
- preferred suppliers
- manually selected suppliers
- suppliers identified through sourcing strategy

A supplier should not automatically be invited simply because it exists in the supplier database.

Qualification and eligibility rules can be used to control participation.

---

# 27. Bid

A **bid** is the supplier's submitted response to an event's commercial or other competitive requirements.

A bid can contain:

```text
Quantity
Price
Currency
Lead Time
Delivery Terms
Payment Terms
Technical Response
Attachments
```

The exact fields depend on event configuration.

---

# 28. Bid Example

Three suppliers bid on 1,000 units:

| Supplier | Unit Price | Delivery | Warranty |
|---|---:|---:|---:|
| Alpha | ₹1,000 | 30 days | 2 years |
| Beta | ₹950 | 45 days | 1 year |
| Gamma | ₹1,025 | 20 days | 3 years |

Lowest price:

```text
Beta
```

But the sourcing team might use weighted scoring:

```text
Price       50%
Quality     20%
Delivery    15%
Warranty    15%
```

The winner should be determined by the configured evaluation methodology and business decision—not simply by lowest price.

---

# 29. Sealed Bidding

In sealed bidding, suppliers submit bids without necessarily seeing competitor prices.

This can be useful when the buyer wants independent submissions rather than real-time competitive price movement.

Always check the event's configured bid visibility and rules.

---

# 30. Multi-Round Bidding

A sourcing event can be conducted in rounds.

Example:

```text
Round 1
10 suppliers
    ↓
Evaluation
    ↓
Shortlist 5
    ↓
Round 2
5 suppliers
    ↓
Negotiation
    ↓
Final bids
    ↓
Award
```

This can be useful when the buyer wants to progressively narrow the competition.

---

# 31. Auction

An auction is a real-time competitive event.

SAP Ariba supports multiple auction formats. The most common procurement scenario is a **reverse auction**, where buyers seek to purchase goods/services and suppliers compete by improving their bids, generally by lowering price.

Example:

```text
Starting price:
₹10,00,000

Supplier A → ₹9,80,000
Supplier B → ₹9,70,000
Supplier C → ₹9,60,000
Supplier A → ₹9,55,000
```

The event continues according to its configured rules and timing.

---

# 32. Reverse Auction

Typical procurement flow:

```text
Buyer wants to BUY
        ↓
Suppliers compete
        ↓
Competitive price decreases
        ↓
Buyer evaluates result
```

Use reverse auctions only when the category and market conditions make competitive price bidding appropriate.

Not every procurement category should be auctioned.

---

# 33. Forward Auction

A forward auction can be used when the organization is selling something.

Example:

```text
Company has excess equipment.

Starting price:
₹5,00,000

Bid A → ₹5,20,000
Bid B → ₹5,40,000
Bid C → ₹5,60,000
```

The highest valid bid may become the leading bid according to the configured auction rules.

---

# 34. English Auction

In an English auction, participants submit progressively competitive bids.

For a reverse procurement auction:

```text
₹1,000
 ↓
₹980
 ↓
₹960
 ↓
₹940
```

Suppliers continue competing according to the event's rules.

---

# 35. Dutch Auction

A Dutch auction changes the price automatically at configured intervals until a participant accepts a price or an event limit is reached.

Conceptually:

```text
₹1,000
  ↓
₹990
  ↓
₹980
  ↓
₹970
  ↓
Supplier accepts
```

There are forward and reverse variants.

---

# 36. Japanese Auction

A Japanese auction presents sequential price levels.

Suppliers accept or reject successive levels according to the auction rules.

Conceptually:

```text
₹1,000
 ↓
₹990  → Supplier A accepts
 ↓
₹980  → Supplier B accepts
 ↓
₹970  → Supplier A exits
```

The exact behavior, visibility, and stopping conditions depend on the configured event.

---

# 37. Auction Formats — Interview Summary

| Format | Core idea |
|---|---|
| English | Participants compete through progressively better bids |
| Dutch | Price changes automatically at intervals until accepted/limit |
| Japanese | Participants accept/reject sequential price levels |
| Reverse auction | Buyer purchases; suppliers generally compete downward on price |
| Forward auction | Seller sells; buyers generally compete upward on price |

Do not confuse **auction direction** with **auction format**.

---

# 38. Auction Preparation

A successful auction requires preparation.

### Before the auction

```text
Define requirement
       ↓
Select eligible suppliers
       ↓
Confirm specifications
       ↓
Define pricing terms
       ↓
Configure event rules
       ↓
Test event
       ↓
Train suppliers
       ↓
Schedule auction
```

### During auction

```text
Monitor participants
Monitor bids
Handle questions
Check timing
Manage erroneous bids according to process
```

### After auction

```text
Analyze results
       ↓
Evaluate commercial + non-commercial criteria
       ↓
Award
       ↓
Contract / downstream process
```

---

# 39. Event Rules

Event rules control event behavior.

Examples include rules for:

- bid visibility
- minimum/maximum bid changes
- timing
- extensions
- participant behavior
- scoring
- currencies
- pricing terms
- auction mechanics

A critical interview point:

> **Event behavior is driven by configuration and event rules.**

Do not assume every customer's event behaves identically.

---

# 40. Lots and Line Items

Large sourcing events may contain multiple line items or lots.

Example:

```text
Lot 1 — Laptops
Lot 2 — Monitors
Lot 3 — Docking Stations
Lot 4 — Support Services
```

A buyer may award different lots to different suppliers.

Example:

```text
Supplier A → Lot 1
Supplier B → Lot 2
Supplier A → Lot 3
Supplier C → Lot 4
```

This is different from assuming that one supplier must win the entire event.

---

# 41. Bid Visibility

The buyer can configure what competitive information participants can see.

Depending on the event configuration, suppliers may see:

- their own rank
- market feedback
- leading bid
- limited competitive information
- no competitor information

Do not assume suppliers can always see competitor prices.

---

# 42. Scoring and Evaluation

Sourcing decisions should consider more than price.

A scoring model might be:

```text
Commercial        50%
Technical         25%
Quality           10%
Delivery          10%
Sustainability     5%
```

Example:

| Supplier | Commercial | Technical | Quality | Delivery | Total |
|---|---:|---:|---:|---:|---:|
| A | 48 | 22 | 8 | 9 | 87 |
| B | 45 | 24 | 10 | 8 | 87 |
| C | 50 | 18 | 7 | 7 | 82 |

The evaluation team then reviews the results and business context before award.

A numerical score is an evaluation mechanism—not automatically the final business decision.

---

# 43. Weighted Scoring

Weighted scoring allows different criteria to contribute differently.

Example:

```text
Price        × 50%
Quality      × 20%
Technical    × 20%
Delivery     × 10%
```

If Supplier A scores:

```text
Price      = 90
Quality    = 80
Technical  = 95
Delivery   = 70
```

Then:

```text
90 × .50 = 45
80 × .20 = 16
95 × .20 = 19
70 × .10 = 7

Total = 87
```

The actual scoring implementation depends on the event configuration.

---

# 44. Supplier Comparison

A sourcing team may compare suppliers across:

```text
Commercial
Technical
Risk
Quality
Delivery
Capacity
Geography
Compliance
Sustainability
```

Example:

```text
Supplier A
Low price
Medium delivery
High technical score

Supplier B
Medium price
Fast delivery
High quality

Supplier C
High price
Very high technical capability
Low risk
```

The correct sourcing decision depends on business requirements.

---

# 45. Award

Award is the point where the buyer decides which supplier(s) receive the business.

Possible outcomes:

```text
Single supplier award
Multiple supplier award
Split award
Partial award
No award
Re-run sourcing event
```

Example:

```text
Requirement = 10,000 units

Supplier A → 6,000
Supplier B → 4,000
```

This is a split award.

---

# 46. Award vs Contract

These are not necessarily the same thing.

### Award

> "Supplier X has been selected for this sourcing event/item."

### Contract

> "The negotiated legal/commercial agreement governing the relationship has been established."

A sourcing event can lead to a contract, but the processes are conceptually distinct.

---

# 47. End-to-End S2C Example

## Scenario: Enterprise Laptop Procurement

### Step 1 — Requirement

```text
5,000 laptops required
```

### Step 2 — Category Strategy

```text
Category:
IT Hardware
```

### Step 3 — Supplier Discovery

Potential suppliers:

```text
Supplier A
Supplier B
Supplier C
Supplier D
Supplier E
```

### Step 4 — Supplier Qualification

Check:

```text
Technical capability
Financial stability
Certifications
Delivery capability
Geographic coverage
```

### Step 5 — RFI

Collect:

```text
Product capability
Support model
Delivery coverage
Certifications
```

Shortlist:

```text
A, B, C
```

### Step 6 — RFP

Request:

```text
Pricing
Warranty
Delivery
Support
Technical compliance
```

### Step 7 — Evaluation

```text
Price       50%
Technical   20%
Warranty    10%
Delivery    10%
Support     10%
```

### Step 8 — Auction

Eligible suppliers participate in a reverse auction.

### Step 9 — Award

```text
Supplier A → 3,000 units
Supplier B → 2,000 units
```

### Step 10 — Contract

Commercial/legal terms are finalized.

### Step 11 — Downstream Procurement

The awarded supplier becomes available for the organization's buying process according to the implementation.

```text
S2C
 ↓
Award / Contract
 ↓
P2O
 ↓
Requisition
 ↓
PO
 ↓
Receipt
 ↓
Invoice
```

---

# 48. SLP + Sourcing Combined Scenario

This is a useful interview scenario.

### Requirement

A company wants to source security services.

```text
Business requirement
       ↓
Supplier Request
       ↓
Registration
       ↓
Qualification
       ↓
Qualified supplier pool
       ↓
RFI
       ↓
RFP
       ↓
Auction / Negotiation
       ↓
Evaluation
       ↓
Award
       ↓
Contract
```

The important distinction is:

```text
SLP
= supplier lifecycle and qualification

Sourcing
= competitive sourcing and supplier selection
```

---

# 49. Supplier Onboarding Failure Scenario

### Problem

Supplier submits registration but cannot proceed.

### Troubleshooting approach

```text
Check registration status
        ↓
Check mandatory questionnaire responses
        ↓
Check validation errors
        ↓
Check approval workflow
        ↓
Check required documents
        ↓
Check supplier contact / invitation
        ↓
Review activity/history
```

Do not immediately assume the problem is technical.

Many supplier onboarding issues are process/configuration/data issues.

---

# 50. Qualification Failure Scenario

### Problem

Supplier believes they are qualified, but they cannot participate in a sourcing event.

Check:

```text
Supplier registration
        ↓
Qualification status
        ↓
Commodity
        ↓
Region
        ↓
Department
        ↓
Event eligibility rules
        ↓
Participant search / invitation
```

A supplier can be qualified for one category/region/department combination and not another.

---

# 51. Supplier Cannot Participate in Event

Possible investigation:

```text
1. Was the supplier invited?
2. Is the supplier eligible?
3. Are prerequisites completed?
4. Has the supplier accepted required agreements?
5. Is the event open?
6. Is the supplier's profile complete?
7. Are required customer-requested profile fields complete?
8. Is the supplier using the correct account/contact?
```

This is a better troubleshooting approach than simply saying "invite the supplier again."

---

# 52. Auction Troubleshooting Scenario

### Supplier says:

> "I cannot submit a bid."

Check:

```text
Event status
      ↓
Supplier participation status
      ↓
Prerequisites
      ↓
Bidder agreement
      ↓
Event timing
      ↓
Required fields
      ↓
Bid rules
      ↓
Currency / pricing terms
      ↓
Network/browser/access issue
```

Always separate:

**business-rule issue** from **configuration issue** from **technical/access issue**.

---

# 53. Common S2C Interview Questions

### Fundamentals

1. What is Source-to-Contract?
2. What is the difference between S2C and P2O?
3. What is strategic sourcing?
4. What is category management?
5. What is a sourcing project?
6. What is a sourcing event?

### SLP

7. What is SAP Ariba SLP?
8. Registration vs qualification?
9. What is supplier onboarding?
10. What is supplier self-registration?
11. What is supplier qualification?
12. What is requalification?
13. What is supplier disqualification?
14. What is preferred supplier management?
15. Can one supplier have different qualification statuses?
16. What is Supplier 360?
17. What information can a supplier questionnaire collect?

### Sourcing

18. What is an RFI?
19. RFI vs RFP?
20. What is an auction?
21. Reverse vs forward auction?
22. What is an English auction?
23. What is a Dutch auction?
24. What is a Japanese auction?
25. What is sealed bidding?
26. What is multi-round bidding?
27. What are lots?
28. What is bid visibility?
29. What are event rules?
30. What is weighted scoring?
31. What is an award?
32. Can multiple suppliers be awarded?
33. Award vs contract?

### Scenario questions

34. Supplier is registered but not qualified. What do you check?
35. Supplier cannot participate in an event. How do you troubleshoot?
36. Supplier cannot submit a bid. What do you check?
37. How would you design an RFP for laptops?
38. When would you use an RFI before an RFP?
39. When would you use an auction?
40. Why shouldn't every category be auctioned?
41. How would you evaluate price vs quality?
42. How would you handle a split award?

---

# 54. Key Terms — Quick Revision

| Term | Meaning |
|---|---|
| S2C | Source-to-Contract |
| SLP | Supplier Lifecycle and Performance |
| Supplier Request | Request to introduce/manage a supplier |
| Registration | Collection/approval of supplier profile information |
| Qualification | Assessment of supplier suitability |
| Requalification | Reassessment of an existing qualification |
| Disqualification | Removal/revocation of qualification |
| Preferred Supplier | Supplier designated as preferred for a defined context |
| Sourcing Project | Framework for a sourcing initiative |
| Sourcing Event | Mechanism for collecting information/bids |
| RFI | Request for Information |
| RFP | Request for Proposal |
| Auction | Real-time competitive event |
| Reverse Auction | Buyer purchases; suppliers compete, generally downward |
| Forward Auction | Seller sells; buyers compete, generally upward |
| Bid | Supplier's submitted event response |
| Lot | Group/item grouping within an event |
| Award | Decision to allocate business |
| Scoring | Evaluation of supplier responses |
| Weighted Scoring | Scoring with different criterion weights |
| Prerequisite | Requirement that must be completed before participation |
| Event Rule | Configuration controlling event behavior |
| Category | Procurement classification |
| Commodity | Classification used in supplier/item processes |
| Supplier 360 | Consolidated supplier profile/view |

---

# 55. S2C Mental Model

Remember S2C as:

```text
                    S2C
                     │
       ┌─────────────┴─────────────┐
       │                           │
     SUPPLIER                   SOURCING
     LIFECYCLE                     │
       │                     ┌─────┴─────┐
       │                     │           │
   Registration              RFI         RFP
       │                                 │
   Qualification                         │
       │                              Auction
   Preferred                            │
       │                                 │
       └──────────────┬──────────────────┘
                      ↓
                   Evaluation
                      ↓
                    Award
                      ↓
                   Contract
                      ↓
                     P2O
```

The key conceptual split is:

> **SLP answers: "Can / should we work with this supplier?"**

> **Sourcing answers: "Which supplier should receive this business, under what commercial proposal?"**

---

# 56. Reference Architecture

A simplified enterprise landscape:

```text
                 BUSINESS USERS
                       │
                       ▼
              SAP ARIBA S2C
                       │
        ┌──────────────┼──────────────┐
        │              │              │
       SLP          Sourcing       Contracts
        │              │              │
        │          RFI/RFP/Auction    │
        │              │              │
        └──────────────┼──────────────┘
                       │
                  Supplier
                  Ecosystem
                       │
                 Business Network
                       │
                       ▼
                  Downstream
                   Procurement
                       │
                       ▼
                  SAP ERP / S4
```

This is a conceptual architecture. Integration specifics belong in the PnI section of this repository.

---

# 57. S2C Implementation Checklist

When implementing an S2C process, consider:

## Business

- What category is being sourced?
- What is the business requirement?
- What is the sourcing strategy?
- Which suppliers are eligible?
- What are the evaluation criteria?
- What is the award strategy?

## Supplier Management

- Is the supplier already registered?
- Is registration required?
- What qualification is required?
- Which questionnaires are needed?
- Who approves supplier information?
- Are requalification rules required?

## Sourcing

- RFI, RFP, auction, or another event?
- What event template?
- What questions?
- What pricing terms?
- What currencies?
- What bid rules?
- What visibility?
- What scoring?
- What deadlines?

## Award

- Single or multiple award?
- Split award?
- Approval required?
- Contract required?
- Downstream supplier enablement?

## Support

- How will users monitor events?
- How will supplier issues be investigated?
- What audit/history is required?
- What data needs to be retained?

---

# 58. Important Distinctions to Remember

### Registration ≠ Qualification

Registration establishes supplier information.

Qualification assesses suitability.

### Qualification ≠ Preferred

A supplier can be qualified without being designated preferred.

### RFI ≠ RFP

RFI primarily gathers information.

RFP gathers structured proposals and commercial information.

### RFP ≠ Auction

RFP allows broader proposal evaluation.

Auction focuses on competitive bidding under configured rules.

### Award ≠ Contract

Award selects business.

Contract formalizes the agreement.

### Supplier ≠ Supplier Qualification

A supplier can exist in the system while having different qualification outcomes for different business contexts.

### Lowest price ≠ Automatic winner

A sourcing decision can consider multiple commercial and non-commercial criteria.

---

# 59. Practical S2C Case Study

## Category

Corporate laptops.

## Requirement

```text
5,000 units
Delivery: India
Warranty: minimum 3 years
Support: onsite
```

## Supplier Lifecycle

```text
Potential Supplier
       ↓
Registration
       ↓
Qualification
       ↓
Qualified
```

## Sourcing

```text
RFI
 ↓
RFP
 ↓
Technical Evaluation
 ↓
Commercial Evaluation
 ↓
Reverse Auction
 ↓
Final Evaluation
 ↓
Award
```

## Result

```text
Supplier A → 3,000 units
Supplier B → 2,000 units
```

## Next step

```text
Award
 ↓
Contract
 ↓
P2O / downstream procurement
```

This single scenario can be reused throughout the guide to connect SLP, Sourcing, Business Network, PnI, and P2O.

---

# 60. What to Learn for an SAP Ariba Interview

For an S2C interview, do not memorize only definitions.

Be able to explain:

1. End-to-end S2C flow.
2. SLP lifecycle.
3. Registration vs qualification.
4. Qualification by business context.
5. Preferred supplier concept.
6. RFI vs RFP.
7. Sourcing project vs sourcing event.
8. Auction formats.
9. Reverse auction.
10. Bid visibility.
11. Event prerequisites.
12. Event rules.
13. Weighted scoring.
14. Supplier evaluation.
15. Award strategies.
16. Split awards.
17. Award vs contract.
18. Supplier onboarding issues.
19. Event participation issues.
20. Auction/bidding troubleshooting.
21. How S2C connects to P2O.
22. How S2C connects to Business Network.
23. Where integration belongs in the architecture.
24. Which behavior is configuration-dependent.

A strong answer should usually follow:

```text
Definition
   ↓
Business purpose
   ↓
Process flow
   ↓
Example
   ↓
Configuration considerations
   ↓
Exception / troubleshooting
```

---


---

# Detailed S2C Expansion

> The following sections extend the existing guide with deeper implementation, support, testing, and interview material while keeping the original concepts and terminology intact.

## D1. S2C Operating Model

```text
STRATEGY
  ↓
Category / Spend / Requirement
  ↓
SUPPLIER LIFECYCLE
  ↓
Request → Registration → Qualification → Requalification
  ↓
SOURCING
  ↓
Request → Project → RFI / RFP / Auction
  ↓
RESPONSE
  ↓
Validation → Evaluation → Scoring
  ↓
DECISION
  ↓
Award → Contract
  ↓
EXECUTION
  ↓
P2O → Business Network → ERP / S4
```

The important idea is that S2C is a connected business lifecycle, not simply an RFP or auction screen.

---

## D2. Business Requirement Analysis

Before creating a sourcing event, establish:

| Area | Questions |
|---|---|
| Requirement | What exactly is being sourced? |
| Category | Which category/commodity is involved? |
| Scope | Which locations, departments and quantities? |
| Timeline | When is the requirement needed? |
| Supplier market | Which suppliers can realistically provide it? |
| Commercial model | Unit price, service rate, subscription, milestone, etc.? |
| Technical requirements | What is mandatory? |
| Compliance | Which certifications or regulatory conditions matter? |
| Evaluation | How will responses be compared? |
| Contract | What terms must survive after award? |
| Downstream | How will the awarded business be purchased? |

### Example

```text
5,000 enterprise laptops
       ↓
Specifications
       ↓
Warranty
       ↓
Delivery
       ↓
Support
       ↓
Supplier eligibility
       ↓
Pricing model
       ↓
Evaluation model
       ↓
Award strategy
```

Do not begin with the event template and discover the business requirement afterward.

---

## D3. Category Strategy vs Sourcing Event

**Category strategy** answers:

> How should this category be managed?

**Sourcing event** answers:

> How will supplier information or bids be collected for this requirement?

Example:

```text
Category Strategy
      ↓
IT Hardware
      ↓
Annual sourcing strategy
      ↓
Laptop requirement
      ↓
RFI
      ↓
RFP
      ↓
Auction
```

A sourcing event is an execution mechanism within a wider procurement strategy.

---

## D4. S2C Business Object Mental Model

Conceptually:

```text
Category
   │
   ├───────────────┐
   ▼               ▼
Supplier       Requirement
   │               │
   ▼               ▼
Registration    Sourcing Request
   │               │
   ▼               ▼
Qualification   Sourcing Project
   │               │
   └───────┬───────┘
           ▼
      Sourcing Event
      ├── RFI
      ├── RFP
      └── Auction
           │
           ▼
      Supplier Response
           │
           ▼
      Evaluation / Scoring
           │
           ▼
          Award
           │
           ▼
        Contract
           │
           ▼
          P2O
```

This is a conceptual relationship. The exact object model and workflow depend on the customer's solution and configuration.

---

## D5. Supplier Lifecycle — Deeper Diagnostic Model

A supplier issue should first be mapped to its lifecycle stage:

```text
Supplier Request
      ↓
Registration
      ↓
Qualification
      ↓
Preferred / Lifecycle Management
      ↓
Sourcing Eligibility
      ↓
Event Participation
```

### Important distinctions

```text
Supplier exists
      ≠
Supplier is registered
      ≠
Supplier is qualified
      ≠
Supplier is preferred
      ≠
Supplier is eligible for a particular event
```

These distinctions are especially useful in support interviews.

---

## D6. Registration Evidence Checklist

When a registration does not progress, capture:

```text
☐ Supplier identity
☐ Registration status
☐ Mandatory questionnaire responses
☐ Validation errors
☐ Required documents
☐ Approval status
☐ Approver information
☐ Invitation/contact information
☐ Activity/history
☐ Timestamp
```

Then classify the issue:

```text
Data
Configuration
Workflow
Supplier action
Access
Process
```

Do not immediately assume the platform is defective.

---

## D7. Qualification Evidence Checklist

For a qualification issue, verify:

```text
Supplier registration
      ↓
Qualification status
      ↓
Commodity
      ↓
Region
      ↓
Department
      ↓
Qualification currency
      ↓
Questionnaire/evidence
      ↓
Event eligibility
```

A supplier may be qualified for one business context while having a different outcome for another.

---

## D8. Sourcing Request vs Project vs Event

| Concept | Main purpose |
|---|---|
| Sourcing Request | Initiates or communicates a sourcing requirement |
| Sourcing Project | Organizes the broader sourcing initiative |
| Sourcing Event | Collects information or competitive responses |

Conceptual flow:

```text
Business
   ↓
Sourcing Request
   ↓
Sourcing Review
   ↓
Sourcing Project
   ├── Tasks
   ├── Documents
   ├── RFI
   ├── RFP
   ├── Auction
   └── Award
```

Exact relationships are configuration-dependent.

---

## D9. Event Design Framework

Before publishing an event, answer five questions:

```text
1. What information do we need?
2. From which suppliers?
3. What makes a response valid?
4. How will responses be evaluated?
5. How will the result become an award?
```

Conceptual event structure:

```text
Event
├── Introduction
├── Prerequisites
├── General Questions
├── Technical Requirements
├── Commercial Requirements
├── Pricing
├── Delivery
├── Compliance
├── Attachments
└── Terms / Conditions
```

---

## D10. Prerequisites vs Questions

### Prerequisite

A prerequisite is primarily an eligibility/access gate.

```text
Accept agreement
      ↓
Complete required prerequisite
      ↓
Provide required evidence
      ↓
Eligible to participate
```

### Event question

A question collects information used during the response/evaluation process.

Example:

```text
Question:
"What is your standard delivery lead time?"

Response:
"30 days"
```

Do not treat every mandatory question as a prerequisite.

---

## D11. RFI Design

The primary purpose of an RFI is to reduce market uncertainty.

Typical sections:

```text
Company
Geography
Capabilities
Certifications
Technology
Service model
References
```

Typical output:

```text
RFI responses
      ↓
Capability comparison
      ↓
Shortlist
      ↓
RFP candidates
```

An RFI should not automatically be described as a price competition.

---

## D12. RFP Design

A practical RFP may contain:

```text
Business requirements
Technical requirements
Commercial requirements
Pricing
Implementation approach
Delivery
Support
SLA
Warranty
Risk / compliance
Attachments
Contract assumptions
```

Example evaluation model:

```text
Commercial   40%
Technical    25%
Delivery     15%
Support      10%
Risk         10%
```

The weights are illustrative; actual event configuration varies.

---

## D13. Pricing Models

Pricing does not have to be a single unit price.

### Unit pricing

```text
Quantity × Unit Price
```

### Tiered pricing

```text
1–100       → Rate A
101–500     → Rate B
501–1000    → Rate C
```

### Service rates

```text
Architect   → Hourly Rate
Consultant  → Hourly Rate
Engineer    → Hourly Rate
```

### Subscription

```text
Implementation
+
Recurring fee
+
Optional services
```

### Total-cost view

```text
Purchase
+
Implementation
+
Support
+
Maintenance
+
Logistics
+
Other defined costs
```

The exact calculation depends on event design.

---

## D14. Bid Collection and Validation

A useful diagnostic sequence is:

```text
Supplier submits
      ↓
Completeness
      ↓
Required fields
      ↓
Prerequisites
      ↓
Commercial response
      ↓
Technical response
      ↓
Attachments
      ↓
Eligibility
      ↓
Evaluation
```

Separate:

```text
Cannot submit
      ≠
Submitted but scored poorly
      ≠
Submitted but excluded by eligibility
```

These are different problem classes.

---

## D15. Auction Readiness

Before using an auction, consider:

```text
Qualified suppliers available?
Comparable specifications?
Comparable commercial terms?
Competitive market?
Clear pricing model?
Supplier readiness?
Business strategy supports auction?
```

A reverse auction is a mechanism, not a universal replacement for an RFP.

---

## D16. Auction vs RFP

| Area | RFP | Auction |
|---|---|---|
| Main purpose | Structured proposal | Competitive bidding |
| Response | Broad | More competitive/event-rule focused |
| Technical evaluation | Common | May happen before/after |
| Competitive visibility | Configurable | Often important |
| Typical fit | Complex requirements | Comparable competitive requirements |

One possible strategy:

```text
RFI
 ↓
RFP
 ↓
Technical qualification
 ↓
Auction
 ↓
Final evaluation
 ↓
Award
```

This is only one possible sourcing strategy.

---

## D17. Lots and Split Awards

Example:

```text
Lot 1 — Laptops
Lot 2 — Monitors
Lot 3 — Docking Stations
Lot 4 — Support
```

Possible result:

```text
Supplier A → Lot 1
Supplier B → Lot 2
Supplier A → Lot 3
Supplier C → Lot 4
```

Split awards can support capacity, geography, risk diversification, specialization, or commercial objectives.

---

## D18. Evaluation Framework

A sourcing evaluation can be organized as:

```text
                 EVALUATION
                     │
       ┌─────────────┼─────────────┐
       ▼             ▼             ▼
   Commercial     Technical       Risk
       │             │             │
     Price        Capability     Compliance
     TCO          Support        Financial
     Terms        Delivery       Regulatory
```

Additional dimensions may include:

```text
Quality
Capacity
Sustainability
Warranty
Service
Geography
Implementation
```

The actual evaluation model is a business/configuration decision.

---

## D19. Weighted Scoring Example

Suppose:

```text
Price        50%
Technical    20%
Delivery     15%
Quality      10%
Risk          5%
```

Supplier A scores:

```text
Price       = 90
Technical   = 80
Delivery    = 90
Quality     = 80
Risk        = 100
```

Calculation:

```text
90 × .50  = 45
80 × .20  = 16
90 × .15  = 13.5
80 × .10  = 8
100 × .05 = 5

Total = 87.5
```

This demonstrates weighted arithmetic only. It does not establish a universal SAP Ariba scoring implementation.

---

## D20. Evaluation vs Award

Keep these concepts separate:

```text
Supplier Responses
      ↓
Evaluation
      ↓
Scores / Comparison
      ↓
Business Review
      ↓
Approval where configured
      ↓
Award
```

Evaluation produces evidence for the decision.

Award allocates the business.

Do not state that the highest numerical score automatically wins unless that is explicitly the configured business process.

---

## D21. Award Models

### Single supplier

```text
100% → Supplier A
```

### Split award

```text
60% → Supplier A
40% → Supplier B
```

### Lot-based award

```text
Lot 1 → Supplier A
Lot 2 → Supplier B
Lot 3 → Supplier C
```

### No award

```text
No acceptable response
        ↓
Revise requirement / re-source
```

---

## D22. S2C → Contract → P2O Boundary

Conceptual flow:

```text
Sourcing Event
      ↓
Final Response
      ↓
Evaluation
      ↓
Award
      ↓
Commercial / Legal Finalization
      ↓
Contract
      ↓
Supplier Enablement
      ↓
P2O
```

Do not state that every award automatically creates a contract. The transition depends on the customer's process and solution configuration.

---

## D23. S2C → Business Network → P2O

The downstream relationship can be remembered as:

```text
S2C
 ↓
Award / Contract
 ↓
P2O
 ↓
Purchase Order
 ↓
Business Network
 ↓
Supplier
```

Depending on architecture, supplier collaboration may involve:

```text
PO
Order Confirmation
ASN
Invoice
```

Exact integration paths belong to the repository's PnI documentation.

---

## D24. Configuration vs Data vs Transaction

### Configuration

Defines process behavior:

```text
Event rules
Templates
Scoring
Workflow
Eligibility rules
```

### Supplier / master data

Represents business information:

```text
Supplier
Category
Region
Department
Contact
Qualification
```

### Transaction/event data

Represents a specific activity:

```text
Sourcing request
Project
RFI
RFP
Bid
Response
Award
```

Diagnostic question:

> Is the issue happening for one supplier, one event, or many?

That often helps identify the fault domain.

---

## D25. S2C Troubleshooting Framework

Use this before changing configuration:

```text
INCIDENT
   ↓
Exact symptom?
   ↓
Lifecycle stage?
   ↓
Who is affected?
   ↓
What changed?
   ↓
Data / configuration / workflow / access / process / integration?
   ↓
What evidence proves the failure point?
   ↓
Corrective action
   ↓
Reprocessing / duplicate-risk check
   ↓
Validation
   ↓
RCA
```

### Common issue classes

```text
Process
Configuration
Supplier data
Workflow
Access / participation
Integration
```

---

## D26. Supplier Registration RCA

### Symptom

Supplier submits registration but cannot progress.

### Investigation

```text
Registration status
      ↓
Mandatory responses
      ↓
Validation
      ↓
Required documents
      ↓
Approval workflow
      ↓
Approver status
      ↓
Supplier contact
      ↓
Activity/history
```

### RCA structure

```text
Problem
Business impact
Evidence
Lifecycle stage
Root cause
Resolution
Validation
Prevention
```

---

## D27. Qualification RCA

### Symptom

Supplier is registered but cannot participate.

### Trace

```text
Registered?
   ↓
Qualified?
   ↓
Correct commodity?
   ↓
Correct region?
   ↓
Correct department?
   ↓
Qualification current?
   ↓
Event eligibility?
   ↓
Invitation / participation?
```

Do not solve a qualification problem by simply re-inviting the supplier.

---

## D28. Event Participation RCA

### Symptom

Supplier cannot open or participate in an event.

Check:

```text
Supplier identity
Participation status
Invitation
Event status
Event timing
Prerequisites
Bidder agreement
Required profile information
Supplier contact
Access/browser evidence
```

Capture the exact error before escalating.

---

## D29. Bid Submission RCA

If the supplier can access the event but cannot submit:

```text
Required fields
      ↓
Pricing fields
      ↓
Currency
      ↓
Bid rules
      ↓
Minimum / maximum changes
      ↓
Timing
      ↓
Conditional questions
      ↓
Attachments
      ↓
Technical/access issue
```

Classify:

```text
Business rule
Configuration
Validation
Access
Technical
```

before changing anything.

---

## D30. Wrong Evaluation Result

Trace:

```text
Supplier response
      ↓
Question value
      ↓
Scoring rule
      ↓
Weight
      ↓
Calculated score
      ↓
Comparison
      ↓
Business interpretation
```

First decide whether the issue is:

```text
Bad data
Bad configuration
Unexpected response
Calculation issue
Business interpretation
```

---

## D31. Approval Troubleshooting

Where approvals are configured:

```text
Who submitted?
      ↓
What object?
      ↓
What values triggered approval?
      ↓
Which rule matched?
      ↓
Who is the approver?
      ↓
Pending / rejected / completed?
      ↓
Did the next stage start?
```

Distinguish:

```text
No workflow
      ≠
Pending workflow
      ≠
Rejected workflow
      ≠
Completed workflow with downstream problem
```

---

## D32. One Supplier vs Many Suppliers

### One supplier affected

Investigate:

```text
Supplier profile
Contact
Qualification
Eligibility
Supplier-specific data
```

### Many suppliers affected

Investigate:

```text
Event configuration
Template
Rules
Workflow
Common data
Platform/service behavior
```

This is a diagnostic heuristic, not a universal rule.

---

## D33. One Event vs Many Events

### One event

Check:

```text
Event-specific rules
Questions
Participants
Timeline
Scoring
```

### Many events

Check:

```text
Shared template
Shared configuration
Workflow
Common master data
Platform/service behavior
```

---

## D34. S2C Test Strategy

A production-ready implementation should test more than the happy path.

```text
Configuration validation
        ↓
Functional testing
        ↓
Integration testing
        ↓
UAT
        ↓
Regression
        ↓
Go-live readiness
```

### Test dimensions

| Dimension | Examples |
|---|---|
| Supplier | New / existing / inactive |
| Qualification | Qualified / pending / expired |
| Event | RFI / RFP / auction |
| Response | Complete / incomplete |
| Scoring | Normal / boundary |
| Award | Single / split |
| Approval | Approve / reject / return |
| Access | Correct / incorrect contact |
| Integration | Success / failure |

---

## D35. S2C Negative Test Pack

```text
☐ Supplier not qualified
☐ Qualification expired
☐ Missing required document
☐ Missing mandatory answer
☐ Failed prerequisite
☐ Invalid pricing value
☐ Invalid currency
☐ Bid outside configured rule
☐ Bid after event closes
☐ Wrong supplier contact
☐ Approver rejects
☐ Approval remains pending
☐ Duplicate supplier request
☐ Integration unavailable
```

Negative tests often expose process weaknesses that happy-path testing misses.

---

## D36. Sample Test Cases

### TC-S2C-001 — Registration

```text
1. Invite supplier.
2. Supplier completes mandatory fields.
3. Supplier submits.
4. Reviewer processes registration.

Expected:
Process advances according to configured workflow.
```

### TC-S2C-002 — Qualification

```text
1. Start qualification.
2. Supplier completes questionnaire.
3. Supplier submits.
4. Reviewer evaluates.

Expected:
Qualification progresses according to configured lifecycle.
```

### TC-S2C-003 — RFP

```text
1. Create RFP.
2. Configure technical/commercial sections.
3. Invite eligible suppliers.
4. Collect responses.
5. Evaluate.

Expected:
Responses can be compared using configured criteria.
```

### TC-S2C-004 — Auction

```text
1. Configure auction.
2. Validate rules.
3. Invite suppliers.
4. Run event.
5. Review result.

Expected:
Event follows configured timing, bidding and visibility rules.
```

### TC-S2C-005 — Split Award

```text
1. Complete evaluation.
2. Allocate quantities.
3. Complete required approval.

Expected:
Award reflects the intended allocation.
```

---

## D37. Cutover Checklist

### Supplier

```text
☐ Supplier population validated
☐ Contacts validated
☐ Categories validated
☐ Qualifications validated
☐ Required documents available
```

### Sourcing

```text
☐ Templates validated
☐ RFI tested
☐ RFP tested
☐ Auction tested where applicable
☐ Questions validated
☐ Pricing validated
☐ Scoring validated
☐ Rules validated
```

### Workflow

```text
☐ Approvers validated
☐ Approval path tested
☐ Rejection tested
☐ Rework tested
```

### Support

```text
☐ Runbook published
☐ Ownership defined
☐ Escalation path defined
☐ Known issues documented
```

---

## D38. Production Support Ownership

A practical conceptual ownership model:

| Area | Typical owner |
|---|---|
| Supplier data | Supplier management / procurement |
| Qualification | Supplier management / category team |
| Event configuration | Sourcing / functional team |
| Workflow | Functional/configuration team |
| Integration | Integration/technical team |
| Access | Security/administration |
| Supplier-side issue | Supplier enablement/network support |
| Business decision | Procurement/sourcing |
| ERP issue | ERP/integration team |

Ownership varies by organization.

---

## D39. S2C Monitoring

Monitor at three levels.

### Business

```text
Open events
Pending supplier responses
Pending approvals
Upcoming deadlines
```

### Process

```text
Registration pending
Qualification pending
Participation issues
Evaluation pending
Award pending
```

### Technical

```text
Integration failures
Service/API failures
Authentication failures
Message failures
```

---

## D40. Useful S2C Metrics

Possible metrics:

```text
Time to onboard supplier
Time to qualify supplier
Supplier response rate
RFP response rate
Auction participation
Sourcing cycle time
Award cycle time
Contract transition time
Supplier participation rate
Savings / negotiated improvement
```

Metrics should be defined according to business objectives and available data.

---

## D41. S2C Incident RCA Template

```markdown
# Incident: <Short title>

## Problem
What happened?

## Business Impact
Who/what was affected?

## Scope
Supplier / event / category / region.

## Symptoms
Exact observed behavior.

## Evidence
Statuses, IDs, timestamps, errors, screenshots where permitted.

## Trace Path
Supplier → eligibility → event → response → evaluation → award.

## Root Cause
What actually caused the issue?

## Resolution
What was changed?

## Validation
How was success confirmed?

## Reprocessing
Was reprocessing required? Was there duplicate risk?

## Prevention
What should prevent recurrence?
```

---

## D42. Practical Lab — Build an RFP

### Requirement

```text
5,000 laptops
India-wide delivery
3-year warranty
Onsite support
```

Design:

```text
1. Supplier prerequisites
2. Technical questions
3. Commercial questions
4. Pricing model
5. Evaluation weights
6. Award strategy
```

Deliverable:

```text
RFP
├── Eligibility
├── Technical
├── Commercial
├── Pricing
├── Evaluation
└── Award
```

---

## D43. Practical Lab — Qualification Matrix

Create:

| Supplier | Commodity | Region | Department | Qualification |
|---|---|---|---|---|
| A | IT Hardware | India | IT | Qualified |
| A | Construction | India | Facilities | Not evaluated |
| B | IT Hardware | India | IT | Pending |
| C | IT Hardware | Germany | IT | Qualified |

Then answer:

```text
Who is eligible for an India IT Hardware event?
Which supplier requires qualification action?
What additional checks are required?
```

---

## D44. Practical Lab — Auction Decision

Given:

```text
Suppliers = 8
Product = standardized laptops
Specifications = comparable
Price = major evaluation factor
Market = competitive
```

Document your reasoning for:

```text
RFI?
RFP?
Auction?
Prerequisites?
Bid visibility?
Evaluation after auction?
Award model?
```

The exercise is about designing a sourcing strategy, not memorizing one correct sequence.

---

## D45. Practical Lab — Production Incident

### Incident

> Supplier can open an RFP but receives an error while submitting the commercial response.

Investigate:

```text
1. Event status
2. Participation
3. Required fields
4. Pricing fields
5. Currency
6. Bid rules
7. Conditional questions
8. Attachments
9. Exact error
10. Technical/access evidence
```

Produce:

```text
Problem
Evidence
Root Cause
Resolution
Validation
Prevention
```

---

## D46. Interview Answer Formula

For most S2C questions:

```text
Definition
   ↓
Business purpose
   ↓
Process flow
   ↓
Example
   ↓
Configuration caveat
   ↓
Exception / troubleshooting
```

### Example — Qualification

```text
Definition:
Qualification assesses supplier suitability.

Purpose:
It determines whether a supplier is suitable for a defined business
context.

Flow:
Supplier → questionnaire → submission → review → decision.

Example:
Cybersecurity + India + Information Security.

Caveat:
The lifecycle and statuses depend on configuration.

Troubleshooting:
Check qualification status, commodity, region, department and
event eligibility.
```

---

## D47. High-Value Interview Scenarios

### 1. Supplier registered but not qualified

Check:

```text
Registration
Qualification
Commodity
Region
Department
Current status
Event eligibility
```

### 2. Supplier cannot participate

Check:

```text
Invitation
Participation
Prerequisites
Event status
Timing
Supplier contact
Eligibility
```

### 3. Supplier cannot bid

Check:

```text
Required fields
Pricing
Currency
Bid rules
Timing
Conditional questions
Exact error
```

### 4. Lowest price supplier was not awarded

Explain that award may consider configured commercial and non-commercial evaluation criteria and the business decision process.

### 5. Why RFI before RFP?

Explain that RFI can reduce uncertainty about supplier capability and market options before a more structured proposal process.

### 6. Why not auction everything?

Explain that auctions are more suitable where suppliers can compete meaningfully under comparable requirements and the market supports that strategy.

---

## D48. One-Page S2C Revision

```text
S2C
│
├── STRATEGY
│   ├── Category
│   ├── Requirement
│   └── Supplier strategy
│
├── SLP
│   ├── Request
│   ├── Registration
│   ├── Qualification
│   ├── Requalification
│   └── Lifecycle
│
├── SOURCING
│   ├── Request
│   ├── Project
│   ├── RFI
│   ├── RFP
│   └── Auction
│
├── EVENT
│   ├── Participants
│   ├── Prerequisites
│   ├── Questions
│   ├── Pricing
│   ├── Rules
│   └── Visibility
│
├── RESPONSE
│   ├── Technical
│   ├── Commercial
│   ├── Bid
│   └── Attachments
│
├── EVALUATION
│   ├── Comparison
│   ├── Scoring
│   └── Weighted criteria
│
├── AWARD
│   ├── Single
│   ├── Multiple
│   ├── Split
│   └── No award
│
└── EXECUTION
    ├── Contract
    ├── P2O
    ├── Business Network
    └── ERP / S4
```

---

## D49. Repository Improvement Plan

The S2C guide should remain the conceptual master guide. Add smaller practical artifacts alongside it rather than endlessly increasing its size.

Recommended future structure:

```text
s2c/
├── README.md
├── sample-rfi.md
├── sample-rfp.md
├── sample-auction.md
├── supplier-qualification-matrix.md
├── weighted-scoring-example.md
├── split-award-example.md
├── supplier-onboarding-rca.md
├── qualification-issue-rca.md
├── event-participation-rca.md
├── auction-bid-rca.md
├── s2c-test-cases.md
└── s2c-interview-scenarios.md
```

This turns the repository from a documentation-only resource into a reusable practice/reference library.

---

## D50. Accuracy Rule

Use this hierarchy when explaining S2C:

```text
Current SAP documentation
        +
Customer configuration
        +
Actual system evidence
        ↓
Conclusion
```

Avoid:

> "SAP Ariba always works this way."

Prefer:

> "This is the conceptual flow; the exact behavior should be verified against the customer's configuration, solution/release, and current SAP documentation."

This is particularly important for production support and consulting interviews.

---

## D51. Final S2C Mental Model

```text
BUSINESS REQUIREMENT
        ↓
CATEGORY STRATEGY
        ↓
SUPPLIER LIFECYCLE
        ↓
REGISTRATION
        ↓
QUALIFICATION
        ↓
SOURCING STRATEGY
        ↓
SOURCING REQUEST
        ↓
SOURCING PROJECT
        ↓
RFI / RFP / AUCTION
        ↓
SUPPLIER RESPONSES
        ↓
EVALUATION / SCORING
        ↓
AWARD
        ↓
CONTRACT
        ↓
DOWNSTREAM PROCUREMENT
        ↓
P2O
        ↓
BUSINESS NETWORK / ERP
```

The core distinctions remain:

> **SLP manages supplier lifecycle and eligibility.**

> **Sourcing manages competitive supplier selection and commercial evaluation.**

> **Award allocates the business.**

> **Contract formalizes the commercial/legal relationship.**

> **P2O executes downstream purchasing.**

---


# 61. Official References

The following SAP documentation should be used to validate product behavior and current capabilities:

### SAP Ariba Strategic Sourcing

- SAP Ariba Strategic Sourcing Solutions:
  https://help.sap.com/docs/ARIBA_SOURCING

- Event Management Guide:
  https://help.sap.com/docs/strategic-sourcing/rfq-and-award-integration-with-sap-ariba-sourcing/4432cc25a8914d3695e06cd995ce6716.html

- SAP Ariba Sourcing Event Process:
  https://help.sap.com/docs/strategic-sourcing/event-management/sap-ariba-sourcing-event-process-7c23b02f71ea1014ac1cc01462d30873

- Guided Sourcing Event Features:
  https://help.sap.com/docs/strategic-sourcing/managing-events-with-guided-sourcing/guided-sourcing-event-features

### Auctions

- SAP Ariba Sourcing Auction Formats:
  https://help.sap.com/docs/strategic-sourcing/event-rules-reference/sap-ariba-sourcing-auction-formats

- About Auctions:
  https://help.sap.com/docs/strategic-sourcing/managing-events-with-guided-sourcing/about-auctions

### Supplier Lifecycle

- Supplier Management Setup and Administration Guide:
  https://help.sap.com/docs/ARIBA_SOURCING/c6163e943b0d48e0885ac73047145cbf

- Supplier Registration Management:
  https://help.sap.com/docs/strategic-sourcing/managing-suppliers-and-supplier-lifecycles/supplier-registration-management

- Supplier Qualifications and Lifecycle Processes:
  https://help.sap.com/docs/strategic-sourcing/managing-suppliers-and-supplier-lifecycles/managing-supplier-qualifications-and-lifecycle-processes

- Supplier Qualification and Disqualification Status Flow:
  https://help.sap.com/docs/strategic-sourcing/managing-suppliers-and-supplier-lifecycles/supplier-qualification-and-disqualification-status-flow

### Supplier participation

- Participating in Sourcing Events:
  https://help.sap.com/docs/business-network-for-trading-partners/participating-in-sourcing-events/participating-in-sourcing-events

---

## Final S2C Checklist

Before considering an S2C implementation or interview preparation complete, you should be able to explain:

```text
☐ S2C lifecycle
☐ Category management
☐ Supplier lifecycle
☐ Supplier request
☐ Supplier registration
☐ Supplier self-registration
☐ Supplier qualification
☐ Qualification questionnaires
☐ Requalification
☐ Disqualification
☐ Preferred suppliers
☐ Supplier profile / 360
☐ Sourcing request
☐ Sourcing project
☐ Sourcing event
☐ RFI
☐ RFP
☐ Event prerequisites
☐ Supplier invitation
☐ Bidding
☐ Sealed bidding
☐ Multi-round bidding
☐ Auction
☐ Reverse auction
☐ Forward auction
☐ English auction
☐ Dutch auction
☐ Japanese auction
☐ Lots
☐ Bid visibility
☐ Event rules
☐ Scoring
☐ Weighted scoring
☐ Supplier comparison
☐ Negotiation
☐ Award
☐ Split award
☐ Contract transition
☐ Supplier onboarding troubleshooting
☐ Qualification troubleshooting
☐ Event participation troubleshooting
☐ Auction troubleshooting
☐ S2C → P2O relationship
☐ S2C → Business Network relationship
☐ S2C → PnI relationship
```

---

## Disclaimer

This is an independent educational guide and is not affiliated with, sponsored by, or endorsed by SAP SE.

SAP, SAP Ariba, SAP Business Network, and related product names are trademarks or registered trademarks of SAP SE or its affiliates.

Examples in this document are fictional and intended for learning. Product behavior, availability, terminology, and configuration can vary by SAP Ariba solution, release, architecture, subscription, and customer configuration. Consult current SAP documentation for implementation-specific decisions.
