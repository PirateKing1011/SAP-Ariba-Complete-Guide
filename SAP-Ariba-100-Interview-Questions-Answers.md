# SAP Ariba Interview — 100 Most-Asked Questions, Answers & Diagrams

> **Purpose:** A practical interview guide for SAP Ariba functional, technical, integration, consulting, and production-support interviews.
>
> **Current terminology:** SAP now uses **SAP Integration Suite, managed gateway for spend management and SAP Business Network** for the capability commonly called CIG. In interviews, it is useful to recognize both terms.
>
> **Study rule:** For each question, learn the **short answer**, then the **why/how**, then the **scenario**. Never claim configuration or production actions you have not actually performed.

---

# PART A — SAP ARIBA FUNDAMENTALS

## 1. What is SAP Ariba?
**Short answer:** SAP Ariba is SAP's cloud procurement and source-to-pay portfolio connecting buying organizations, suppliers, procurement processes, and supplier collaboration.

**Explanation:** It covers buying/procurement, invoicing, sourcing, contracts, supplier management, APIs, and supplier collaboration through SAP Business Network.

**Diagram**
```text
Business Need
     ↓
SAP Ariba
 ┌───┼───────────────┐
Buying  Sourcing  Contracts
  │
Invoicing ── Supplier Management
  │
  ↓
SAP Business Network
```

## 2. What are the major SAP Ariba solutions/capabilities?
Know these areas:
- Buying / Guided Buying
- Buying and Invoicing
- Sourcing
- Contracts
- Supplier Management
- SAP Business Network
- APIs / extensibility
- Managed Gateway integration

## 3. What is Source-to-Pay?
**Answer:** Source-to-Pay covers the lifecycle from identifying a sourcing requirement through supplier selection, contracting, purchasing, receiving, invoicing, and payment.

```text
Sourcing → Contract → Requisition → PO → Receipt → Invoice → Payment
```

## 4. What is Procure-to-Pay?
**Answer:** P2P starts with the purchasing requirement and runs through requisition, approval, purchase order, fulfillment/receipt, invoice reconciliation and payment.

## 5. What is SAP Business Network?
**Answer:** It is the collaboration network connecting buying organizations and suppliers for business document exchange and supplier collaboration.

```text
Buyer ERP / Ariba
       ↓
SAP Business Network
       ↓
Supplier
```

## 6. What is the difference between SAP Ariba and SAP Business Network?
**Answer:** Ariba applications provide procurement/sourcing/contracting processes; SAP Business Network provides the trading-partner collaboration and document exchange layer.

## 7. What is Guided Buying?
**Answer:** Guided Buying provides a guided user experience for finding and requesting goods/services through approved procurement channels, catalogs, forms and policies.

## 8. What is a catalog?
**Answer:** A catalog contains supplier product/service information such as description, supplier part number, price, unit of measure and category.

```text
Supplier Catalog
      ↓
Catalog validation
      ↓
Buyer catalog
      ↓
User search
      ↓
Requisition
```

## 9. What is PunchOut?
**Answer:** PunchOut allows a buyer to leave the procurement interface for a supplier-hosted catalog and return the selected cart to the buying application.

```text
Ariba → PunchOut → Supplier Catalog
                     ↓
                 Shopping Cart
                     ↓
Ariba ← Cart Return ← Supplier
```

## 10. What is CIF?
**Answer:** CIF, or Catalog Interchange Format, is a catalog data format used for exchanging catalog content. Understand its structure and where catalog integration fits; do not confuse CIF with cXML transaction documents.

---

# PART B — P2P

## 11. Explain the complete P2P process.
**Answer:**
```text
Need
 ↓
Purchase Requisition
 ↓
Approval
 ↓
Purchase Order
 ↓
Supplier
 ↓
Confirmation / Ship Notice
 ↓
Goods Receipt
 ↓
Invoice
 ↓
Invoice Reconciliation
 ↓
ERP / Payment
```

## 12. What is a Purchase Requisition?
**Answer:** An internal request to procure goods or services.

## 13. PR vs PO?
| PR | PO |
|---|---|
| Internal request | Formal order |
| Represents need | Represents purchasing commitment |
| Approval-driven | Supplier-facing |
| Precedes PO | Sent to supplier |

## 14. What happens when a PR is submitted?
**Answer:** The system validates the requisition, evaluates applicable workflow/approval rules, and routes it for approval where required.

## 15. How does approval workflow work?
**Answer:** Approval rules can evaluate factors such as amount, commodity, requester, cost center, purchasing organization, or other configured attributes.

```text
PR
 ↓
Rule Evaluation
 ├─ Auto approval
 └─ Approver(s)
      ↓
   Approved
```

## 16. What if a PR is stuck in approval?
**Answer:** Check PR status, approval history, current approver, rule evaluation, user/organizational data, delegation/substitution, and whether the workflow needs correction or resubmission.

## 17. What is a Purchase Order?
**Answer:** A formal purchasing document sent to a supplier specifying what is being ordered and under which commercial/delivery conditions.

## 18. What happens after PO creation?
**Answer:** Depending on configuration, the PO is transmitted to the supplier through SAP Business Network or another enabled channel. The supplier may confirm, reject, or fulfill it.

## 19. What is a PO flip invoice?
**Answer:** A supplier creates an invoice based on an existing PO, typically using the PO information to reduce manual entry and improve matching.

## 20. What is a service purchase?
**Answer:** A procurement transaction for services rather than physical goods. Receipt/confirmation concepts can differ from material goods and may involve service entry/acceptance processes.

## 21. What is a Goods Receipt?
**Answer:** A record that goods have been received. It can be partial.

```text
PO = 100
GR = 80
Remaining = 20
```

## 22. What is partial receipt?
**Answer:** Receiving less than the ordered quantity, with later receipts potentially completing the order.

## 23. What is an Order Confirmation?
**Answer:** A supplier response acknowledging or proposing changes to the purchase order, such as quantity or delivery date.

## 24. What is a Ship Notice / ASN?
**Answer:** A supplier message providing shipment information before or around delivery, such as quantities and shipping details.

## 25. How would you troubleshoot a PO not reaching a supplier?
**Answer:**
1. Confirm PO exists and is released.
2. Check transmission status.
3. Check supplier relationship/network setup.
4. Check transaction/payload status.
5. Check integration endpoint and mapping.
6. Check Business Network.
7. Check relevant ERP/integration logs.
8. Reprocess only after identifying the cause.

---

# PART C — INVOICING & RECONCILIATION

## 26. What invoice types should you know?
Know:
- PO-based invoice
- Non-PO invoice
- Credit memo
- Debit memo
- Service-related invoices
- Contract-based invoices where applicable

## 27. What is invoice reconciliation?
**Answer:** It is the process of validating invoice charges against purchasing/receiving information and applying business rules/tolerances to determine whether exceptions require resolution.

```text
PO ──────┐
         ├→ Reconciliation → Approved / Exception
Receipt ─┤
         │
Invoice ─┘
```

## 28. What is 2-way matching?
**Answer:** Conceptually, invoice values are compared with the purchase order.

```text
PO ↔ Invoice
```

## 29. What is 3-way matching?
**Answer:** The invoice is evaluated against the purchase order and receipt information.

```text
        PO
       /        /     Receipt ↔ Invoice
```

## 30. What causes an invoice exception?
Common causes:
- Quantity variance
- Price variance
- Tax variance
- Shipping variance
- Missing receipt
- Duplicate invoice
- Invalid/mismatched PO
- Supplier/master-data issue
- Tolerance exceeded

## 31. What is a tolerance?
**Answer:** A configured business allowance for acceptable variance, such as a small price or quantity difference.

## 32. How would you troubleshoot a blocked invoice?
**Answer:**
```text
Invoice
 ↓
Status
 ↓
Reconciliation / Exception
 ↓
Identify variance
 ↓
Check PO
 ↓
Check receipt
 ↓
Check supplier/master data
 ↓
Check rule/tolerance
 ↓
Correct root cause
 ↓
Reconcile/reprocess
```

## 33. PO quantity is 100, receipt is 80 and invoice is 100. What happens?
**Answer:** A quantity discrepancy can be identified because the invoiced quantity exceeds the received quantity. Whether it blocks approval depends on configured rules and tolerances.

## 34. PO price is ₹1,000 but invoice price is ₹1,100. What do you check?
**Answer:** Check PO pricing, invoice line price, currency, tax/freight/discount components, contract conditions if relevant, and configured price tolerances.

## 35. What is a Non-PO invoice?
**Answer:** An invoice not directly associated with a purchase order. It requires appropriate accounting and approval controls because normal PO-based matching is unavailable.

## 36. What is a credit memo?
**Answer:** A document reducing an amount previously invoiced, typically because of returns, corrections, overbilling or other adjustments.

## 37. What is a debit memo?
**Answer:** A document increasing an amount owed under applicable business scenarios.

## 38. What happens after an invoice is approved?
**Answer:** Depending on the landscape, invoice information/status can flow toward the ERP/payment process. The exact downstream payment process belongs to the customer's ERP/finance design.

## 39. How can suppliers create invoices on SAP Business Network?
**Answer:** Depending on configuration, suppliers can use online invoice creation/PO flip, cXML `InvoiceDetailRequest`, or supported EDI methods. SAP documentation describes these channels and validation rules.

## 40. How do you investigate a supplier invoice that never arrived?
**Answer:** Determine whether the supplier submitted it, whether Business Network accepted/validated it, whether it was routed to the buyer, whether the buyer application created the invoice, and whether integration/ERP processing failed.

---

# PART D — BUSINESS NETWORK & SUPPLIERS

## 41. What is a supplier relationship?
**Answer:** It establishes the buyer-supplier relationship and enables permitted transactions/collaboration between the parties.

## 42. What is supplier onboarding?
**Answer:** The process of inviting, registering, validating, enabling and preparing a supplier to transact with the buying organization.

```text
Invite
 ↓
Register
 ↓
Validate
 ↓
Enable
 ↓
Test
 ↓
Transact
```

## 43. What is supplier enablement?
**Answer:** Making a supplier technically and operationally ready to receive/send the required documents through the chosen channel.

## 44. What supplier information is important?
Examples:
- Legal identity
- Addresses
- Tax information
- Payment information
- Contact information
- Network/account information
- Purchasing/ERP identifiers

## 45. Supplier cannot see a PO. What do you check?
**Answer:**
1. PO status/release.
2. Supplier assignment.
3. Trading relationship.
4. Business Network account.
5. Transmission status.
6. Document routing.
7. Supplier account/user access.
8. Integration transaction status.

## 46. What is supplier qualification?
**Answer:** Evaluating whether a supplier meets defined business, operational, compliance, risk or capability criteria.

## 47. What is supplier performance?
**Answer:** Measuring supplier performance using defined metrics such as delivery, quality, responsiveness or other organization-specific KPIs.

## 48. What is supplier risk?
**Answer:** Assessment and monitoring of supplier-related business risks such as financial, operational, compliance or supply-chain risk.

## 49. What is a trading partner?
**Answer:** A business entity exchanging transactions/documents with another organization through the network.

## 50. Why is SAP Business Network important in P2P?
**Answer:** It provides a collaboration and transaction exchange layer between buying organizations and suppliers, reducing manual exchange and enabling electronic document visibility.

---

# PART E — INTEGRATION / MANAGED GATEWAY / CIG

## 51. What is CIG?
**Answer:** CIG is the commonly used historical abbreviation for Cloud Integration Gateway. Current SAP terminology is **SAP Integration Suite, managed gateway for spend management and SAP Business Network**.

## 52. Why is Managed Gateway used?
**Answer:** It supports integration between SAP spend/procurement solutions, SAP Business Network and backend systems for supported business processes and document exchange.

## 53. Explain the integration architecture.
```text
SAP ECC / S/4HANA
        ↓
Integration / Managed Gateway
        ↓
SAP Business Network
        ↓
Supplier
```

The exact architecture depends on the customer's SAP landscape and integration scenario.

## 54. What is an endpoint?
**Answer:** An endpoint identifies the destination/channel through which a transaction is routed. In Business Network integration, endpoint configuration helps route documents to the appropriate external destination.

## 55. What is inbound vs outbound?
**Answer:** Always define the perspective. From the ERP perspective, an outbound PO is leaving ERP; from the receiving system's perspective, that same document is inbound.

## 56. What is mapping?
**Answer:** Mapping transforms source-system fields/values into the structure and values expected by the target system.

```text
ERP Field
   ↓
Mapping
   ↓
cXML / Target Field
```

## 57. What is a cXML document?
**Answer:** cXML is an XML-based format used for business document exchange in procurement/trading-partner scenarios.

## 58. Name important cXML documents.
Know:
- `OrderRequest`
- `OrderResponse`
- `ConfirmationRequest`
- `ShipNoticeRequest`
- `InvoiceDetailRequest`
- `StatusUpdateRequest`
- `PunchOutSetupRequest`

## 59. What is `OrderRequest`?
**Answer:** A cXML business document representing an order/purchase-order transaction sent in supported procurement network scenarios.

```text
Buyer
 ↓
OrderRequest
 ↓
Business Network
 ↓
Supplier
```

## 60. What is `InvoiceDetailRequest`?
**Answer:** A cXML document used to represent invoice details in supported invoice integration scenarios.

## 61. What is `StatusUpdateRequest`?
**Answer:** A cXML status message used to communicate transaction status updates in supported flows.

## 62. What is Cloud Connector?
**Answer:** SAP Cloud Connector provides controlled connectivity between SAP cloud applications and selected on-premise systems, depending on the architecture.

## 63. How do you troubleshoot a failed integration transaction?
**Answer:**
```text
Business Document
 ↓
Transaction Status
 ↓
Payload
 ↓
Endpoint
 ↓
Authentication
 ↓
Mapping
 ↓
Master Data
 ↓
Middleware / Gateway
 ↓
ERP Logs
 ↓
Reprocess
```

## 64. What logs/tools do you check?
**Answer:** It depends on the landscape. Explain the actual tools available in the customer's environment. In SAP ERP integration scenarios, relevant application/interface logs may include SAP application logs and integration-specific monitoring. Do not claim a specific log was checked unless you actually used it.

## 65. What is `SLG1`?
**Answer:** SAP application log transaction used to display application logs. In relevant managed-gateway/ERP integration scenarios, SAP documentation references integration-specific objects/subobjects; use the customer's documented configuration rather than assuming one universal object.

---

# PART F — MASTER DATA

## 66. What is master data?
**Answer:** Relatively stable reference data used across transactions.

Examples:
- Supplier
- Material
- Plant
- Company Code
- Purchasing Organization
- Purchasing Group
- Cost Center
- Currency
- Payment Terms
- Tax information

## 67. Master data vs transactional data?
```text
Master Data
Supplier / Material / Org Data
        ↓
Transactional Data
PR / PO / Receipt / Invoice
```

## 68. Why is master data important in integration?
**Answer:** Transactions depend on correct identifiers and values. A technically successful message can still fail business processing if master data is missing or inconsistent.

## 69. How do you troubleshoot a master-data-related error?
**Answer:**
1. Identify the failing field/value.
2. Identify source system.
3. Verify source data.
4. Check mapping/transformation.
5. Check target data.
6. Correct the appropriate source/configuration.
7. Reprocess and validate.

## 70. What organizational data should an Ariba consultant understand?
Know concepts such as:
- Company code
- Purchasing organization
- Purchasing group
- Plant/facility
- Cost center
- Commodity/category
- Accounting information

---

# PART G — SOURCING / CONTRACTS

## 71. What is SAP Ariba Sourcing?
**Answer:** A sourcing capability used to run structured supplier sourcing events and evaluate responses for sourcing decisions.

## 72. RFI vs RFP vs RFQ?
| Type | Purpose |
|---|---|
| RFI | Gather information |
| RFP | Request proposals |
| RFQ | Request pricing/quotations |

## 73. What is an auction?
**Answer:** A competitive sourcing event where suppliers submit bids under defined rules and time constraints.

## 74. What is an award?
**Answer:** The sourcing decision allocating business to selected supplier(s) based on evaluation criteria.

## 75. Explain sourcing-to-contract.
```text
Requirement
 ↓
RFI/RFP/RFQ
 ↓
Supplier Responses
 ↓
Evaluation
 ↓
Award
 ↓
Contract
 ↓
Procurement
```

## 76. What is SAP Ariba Contracts?
**Answer:** A contract lifecycle capability supporting contract creation/authoring, review, approval, execution and ongoing management.

## 77. What is contract compliance?
**Answer:** Ensuring purchasing and supplier behavior aligns with negotiated contract terms, pricing, quantities, dates and other obligations.

## 78. How can contracts influence procurement?
**Answer:** Contracts can provide negotiated terms and commercial controls that influence purchasing and invoice validation depending on the configured solution/process.

---

# PART H — APIs / TECHNICAL

## 79. What is an API?
**Answer:** An API is a programmatic interface allowing software systems to communicate with a service.

## 80. API vs cXML?
**Answer:** cXML is a business document format; an API is an interface through which software accesses or submits functionality/data. cXML documents can be transported through supported APIs/channels.

## 81. What HTTP methods should you know?
```text
GET     → Retrieve
POST    → Create/submit
PUT     → Replace/update
PATCH   → Partial update
DELETE  → Delete
```

## 82. Common HTTP status codes?
```text
200 Success
201 Created
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
409 Conflict
429 Rate Limited
500 Server Error
503 Service Unavailable
```

## 83. How do you troubleshoot an API failure?
```text
Endpoint
 ↓
Authentication
 ↓
Authorization
 ↓
Headers
 ↓
Payload
 ↓
Parameters
 ↓
HTTP response
 ↓
Server/application logs
```

## 84. What is authentication vs authorization?
**Authentication:** Who are you?

**Authorization:** What are you allowed to do?

## 85. What is idempotency?
**Answer:** The ability to repeat an operation without unintentionally creating duplicate business effects. It is particularly important when integrations retry transactions.

---

# PART I — PRODUCTION SUPPORT

## 86. What is your production incident approach?
**Answer:**
```text
Incident
 ↓
Business Impact
 ↓
Transaction Identification
 ↓
Reproduce / Trace
 ↓
Root Cause
 ↓
Workaround
 ↓
Permanent Fix
 ↓
Validation
 ↓
RCA
```

## 87. Incident vs problem vs change?
| Term | Meaning |
|---|---|
| Incident | Something has failed / service is impacted |
| Problem | Underlying cause of one or more incidents |
| Change | Controlled modification to the system |

## 88. How do you prioritize incidents?
Consider:
- Business impact
- Number of users
- Financial impact
- Payment impact
- Supplier impact
- Production/non-production
- Workaround
- SLA

## 89. What makes a good RCA?
Include:
- Problem statement
- Business impact
- Timeline
- Root cause
- Contributing factors
- Resolution
- Preventive action

## 90. How do you handle an escalation?
**Answer:** First understand the business impact and facts, communicate clearly, avoid speculation, involve the right technical/functional owners, maintain a timeline, and confirm the resolution with evidence.

---

# PART J — CONSULTING QUESTIONS

## 91. How do you gather requirements?
**Answer:**
```text
Business Goal
 ↓
Current Process
 ↓
Pain Point
 ↓
Business Rules
 ↓
Volume / Users
 ↓
Integration Landscape
 ↓
Standard SAP Capability
 ↓
Gap Analysis
 ↓
Solution
```

Ask:
- What is the current process?
- Who performs it?
- What is the business problem?
- What is the desired outcome?
- What systems are involved?
- What approvals are required?
- What exceptions exist?

## 92. What is fit-to-standard?
**Answer:** First evaluate whether standard SAP functionality satisfies the requirement before considering customization or extensions.

## 93. What is gap analysis?
**Answer:** Comparing the customer's required process with standard product capability and identifying differences that need configuration, process change, integration or extension.

## 94. How would you handle a requirement that standard Ariba does not support?
**Answer:**
1. Clarify the real business need.
2. Confirm standard capability.
3. Check configuration options.
4. Consider process redesign.
5. Evaluate integration/extension options.
6. Assess cost, risk and maintainability.
7. Present alternatives to the customer.

## 95. How do you handle a difficult client?
**Answer:** Focus on facts and business impact, listen carefully, clarify the requirement, set realistic expectations, document decisions, communicate progress, and escalate constructively when required.

---

# PART K — SCENARIO QUESTIONS

## 96. A PO was created but the supplier did not receive it. Walk me through it.

**Strong answer:**

> "I would first confirm that the PO was created, approved/released and eligible for transmission. Then I would check the transmission status and determine whether the document reached the integration layer or SAP Business Network. If it failed, I would inspect the transaction details and payload, validate supplier/network configuration, endpoint and mapping, and check relevant application/integration logs. Once the root cause is identified, I would correct it and reprocess if appropriate, then validate successful supplier receipt."

## 97. An invoice is blocked. What do you do?

**Strong answer:**

> "I would not immediately reprocess it. First I would identify the invoice reconciliation status and exact exception. Then I would compare the invoice against the PO and receipt, check price/quantity/tax/freight and configured tolerances, and verify relevant supplier or master data. After identifying the root cause, I would coordinate the correction with the appropriate owner, reconcile/reprocess as applicable, and validate the final status."

## 98. A supplier says their invoice was submitted but the buyer cannot see it. What do you check?

**Strong answer:**

> "I would trace the document from the supplier submission point. First I would confirm the supplier actually submitted it and capture the invoice/document identifier. Then I would check Business Network validation and status, routing to the buyer, buyer application creation, and any integration transaction or ERP errors. This lets me determine whether the issue is supplier-side, network-side, application-side, or integration-side."

## 99. A client asks you to customize everything. What do you do?

**Strong answer:**

> "I would first understand the business outcome rather than accepting the requested technical solution. I would check whether standard functionality or configuration can meet the requirement, then consider process changes. If there is a genuine gap, I would evaluate integration or extension options and explain the trade-offs in cost, maintenance, upgrade impact and complexity. The objective is a sustainable solution rather than customization for its own sake."

## 100. Tell me about your SAP Ariba experience.

**Recommended structure:**

```text
Current Role
     ↓
Ariba Area
     ↓
P2P Exposure
     ↓
Support / Incident Handling
     ↓
Integration Exposure
     ↓
Troubleshooting / RCA
     ↓
Current Technical Growth
```

**Sample answer — customize this to your real experience:**

> "I have experience working in SAP Ariba support with a focus on procurement and P2P-related processes. My understanding covers requisitions, approvals, purchase orders, supplier collaboration, invoicing and reconciliation, along with integration and production-support concepts. When investigating an issue, I start with the business impact and transaction status, trace the process and integration points, validate master data and relevant logs, identify the root cause and then validate the resolution. I'm also strengthening my technical skills in cXML, APIs, integration and Python so that I can contribute more deeply to technical troubleshooting and consulting activities."

**Important:** Do not claim configuration, integration development or production activities you did not personally perform. Explain your actual exposure and then clearly state what you understand conceptually.

---

# FINAL RAPID-REVISION MAP

## P2P

```text
PR
 ↓
Approval
 ↓
PO
 ↓
Confirmation
 ↓
Ship Notice
 ↓
Receipt
 ↓
Invoice
 ↓
Reconciliation
 ↓
Approval
 ↓
ERP / Payment
```

## Integration

```text
ERP / S4
   ↓
Integration / Managed Gateway
   ↓
SAP Business Network
   ↓
Supplier
```

## Troubleshooting

```text
Issue
 ↓
Business Impact
 ↓
Transaction Status
 ↓
Document / Payload
 ↓
Master Data
 ↓
Mapping
 ↓
Endpoint
 ↓
Integration Logs
 ↓
Root Cause
 ↓
Fix
 ↓
Reprocess
 ↓
Validate
```

## Consulting

```text
Requirement
 ↓
Current Process
 ↓
Pain Point
 ↓
Standard Capability
 ↓
Fit-to-Standard
 ↓
Gap
 ↓
Solution Options
 ↓
Impact / Risk
 ↓
Implementation
```

# LAST-MINUTE PRIORITY

If you have very little time, master these first:

1. P2P end-to-end
2. PR vs PO
3. Approval workflow
4. SAP Business Network
5. Invoice reconciliation
6. 2-way / 3-way matching
7. Invoice exceptions
8. CIG / Managed Gateway
9. cXML
10. `OrderRequest`
11. `InvoiceDetailRequest`
12. Integration troubleshooting
13. Master data
14. Production incident/RCA
15. Requirement gathering
16. Fit-to-standard
17. Scenario: PO not reaching supplier
18. Scenario: invoice blocked
19. Scenario: invoice not reaching ERP
20. Your actual SAP Ariba experience

---

## Current SAP terminology and source notes

This guide intentionally uses current SAP terminology. SAP's current documentation uses **SAP Integration Suite, managed gateway for spend management and SAP Business Network** and documents endpoint-based integration, cXML document types, Business Network invoicing, and master-data integration. citeturn0search0turn0search6turn0search4turn0search9

SAP's documentation describes supplier invoice creation through online invoice functionality and supported cXML/EDI channels, including `InvoiceDetailRequest`, and describes Business Network validation and invoice lifecycle behavior. citeturn0search14turn0search4

Use official SAP Help documentation as the authority for customer-specific configuration, current feature behavior, release-dependent details, and integration prerequisites.
