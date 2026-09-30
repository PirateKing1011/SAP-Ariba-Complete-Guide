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
