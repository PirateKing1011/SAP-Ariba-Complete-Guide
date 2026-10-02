# SAP Ariba Practical Interview Questions & Answers

> **Purpose:** A practical, scenario-heavy interview preparation guide for SAP Ariba functional consultants, P2P consultants, integration/support engineers, SAP MM-aware consultants, implementation teams, and production-support professionals.

> **Current terminology:** SAP currently uses **SAP Integration Suite, managed gateway for spend management and SAP Business Network** for the capability commonly known as CIG. In interviews, recognize both terms.

> **Study rule:** Learn the short answer first, then understand the reasoning, then practice the scenario. Never claim configuration, development, monitoring, or production actions you have not personally performed.

---

# How to Use This Guide

For every technical question, structure your answer as:

```text
1. What is it?
       ↓
2. Why is it used?
       ↓
3. Where does it fit?
       ↓
4. How does it work?
       ↓
5. What can fail?
       ↓
6. How would I troubleshoot it?
```

For scenario questions:

```text
Business Impact
      ↓
Identify Document / ID
      ↓
Identify Direction
      ↓
Trace Transaction
      ↓
Find Failure Layer
      ↓
Check Payload / Mapping / Master Data
      ↓
Check Application Logs
      ↓
Identify Root Cause
      ↓
Fix
      ↓
Reprocess Safely
      ↓
Validate
      ↓
Document RCA
```

---

# PART A — SAP ARIBA FUNDAMENTALS

## 1. What is SAP Ariba?

**Short answer:** SAP Ariba is SAP's cloud procurement and source-to-pay portfolio connecting buying organizations, suppliers, procurement processes, and supplier collaboration.

**Interview follow-up:** What areas have you worked with?

Mention only your real exposure, but understand:

- Buying
- Guided Buying
- Sourcing
- Contracts
- Supplier Management
- Buying and Invoicing
- SAP Business Network
- Integration
- APIs

---

## 2. What is SAP Business Network?

**Answer:** It is the collaboration and transaction network connecting buying organizations and suppliers for supported business-document exchange and supplier collaboration.

```text
Buyer
  ↓
SAP Ariba / ERP
  ↓
SAP Business Network
  ↓
Supplier
```

---

## 3. SAP Ariba vs SAP Business Network?

| SAP Ariba | SAP Business Network |
|---|---|
| Procurement/sourcing applications | Trading-partner collaboration network |
| Buying | Supplier collaboration |
| Guided Buying | PO/document exchange |
| Sourcing | Confirmations |
| Contracts | ASN |
| Supplier processes | Invoices / transaction exchange |

---

## 4. What is Source-to-Pay?

**Answer:**

```text
Sourcing
   ↓
Supplier Selection
   ↓
Contract
   ↓
Requisition
   ↓
PO
   ↓
Receipt
   ↓
Invoice
   ↓
Payment
```

---

## 5. What is P2P?

**Answer:** Procure-to-Pay covers the purchasing lifecycle from requirement/requisition through approval, PO, fulfillment/receipt, invoicing, reconciliation and payment.

---

## 6. What is P2O?

**Answer:** In this repository, P2O refers to the procurement execution layer around requisition, approval, purchasing, and related procurement processing.

---

## 7. What is Guided Buying?

**Answer:** A guided procurement experience that helps users purchase through approved catalogs, forms, policies, and procurement channels.

---

## 8. What is a catalog?

**Answer:** Structured supplier product/service information used by buyers to search and select items.

Typical information:

- Supplier
- Supplier part number
- Description
- Price
- Currency
- UOM
- Category
- Contract/reference information

---

## 9. CIF vs cXML?

**Answer:**

- **CIF** is a catalog interchange format.
- **cXML** is an XML-based business transaction/document format.

Do not describe them as interchangeable.

---

## 10. What is PunchOut?

**Answer:** PunchOut allows a buyer to navigate from the procurement application to a supplier-hosted shopping experience, select items, and return the cart to the procurement application.

```text
Ariba
  ↓
PunchOut
  ↓
Supplier Website
  ↓
Shopping Cart
  ↓
Ariba
```

---

# PART B — P2P / PROCUREMENT

## 11. Explain the complete P2P flow.

```text
Business Need
      ↓
Purchase Requisition
      ↓
Approval
      ↓
Purchase Order
      ↓
Supplier
      ↓
Confirmation
      ↓
ASN / Shipment
      ↓
Goods Receipt
      ↓
Invoice
      ↓
Reconciliation
      ↓
ERP / Payment
```

---

## 12. PR vs PO?

| PR | PO |
|---|---|
| Internal purchasing request | Formal purchasing document |
| Represents requirement | Represents order/commitment |
| Approval-driven | Supplier-facing |
| Precedes purchasing execution | Sent to supplier |

---

## 13. What happens when a PR is submitted?

**Answer:** The application validates the requisition and evaluates applicable approval/workflow rules. Depending on configuration, it may route through one or more approvers before purchasing execution.

---

## 14. What attributes can influence approval?

Examples can include:

- Amount
- Requester
- Commodity/category
- Cost center
- Company code
- Purchasing organization
- Accounting data
- Custom business attributes

Always say **"depending on configured rules."**

---

## 15. PR is stuck in approval. What do you check?

**Strong answer:**

1. PR status
2. Approval history
3. Current approver
4. Rule evaluation
5. Approver/user validity
6. Delegation/substitution
7. Organizational/master data
8. Workflow configuration
9. Whether the request requires correction/resubmission
10. Relevant application logs

---

## 16. PO was created but not transmitted. What do you check?

```text
PO Created?
   ↓
Approved / Released?
   ↓
Eligible for Transmission?
   ↓
Output / Transmission Status?
   ↓
Integration Transaction?
   ↓
Business Network?
   ↓
Supplier?
```

---

## 17. What happens after PO creation?

**Answer:** Depending on architecture and configuration, the PO can be transmitted through SAP Business Network or another enabled supplier channel. The supplier can then confirm, reject, or fulfill it.

---

## 18. What is an Order Confirmation?

**Answer:** A supplier response acknowledging a PO or proposing changes such as quantity, price, or delivery information, depending on the supported process.

---

## 19. What is an ASN?

**Answer:** An Advance Ship Notice provides shipment-related information before or around delivery.

---

## 20. What is a Goods Receipt?

**Answer:** A record that goods were received by the buyer/ERP process. Receipt can be partial.

```text
PO = 100
GR = 80
Remaining = 20
```

---

## 21. What is partial receipt?

**Answer:** Receiving less than the ordered quantity, with additional receipts potentially completing the remaining quantity.

---

## 22. What is service procurement?

**Answer:** Procurement of services rather than physical goods. Confirmation/receipt may involve service acceptance or service-entry processes rather than a normal material goods receipt.

---

## 23. What is PO flip?

**Answer:** A supplier uses an existing PO as the basis for creating a related downstream document, commonly an invoice, reducing manual entry.

---

## 24. PO exists but supplier says they cannot see it. Walk me through it.

**Strong answer:**

> "I would first confirm the PO exists and is approved/released. Then I would check supplier assignment, transmission status, Business Network routing, trading relationship, supplier account, and document status. If the document left the source application, I would trace the integration transaction and payload, then check the relevant endpoint, mapping, and application logs. I would identify the failure layer before reprocessing."

---

## 25. How do you prove whether the PO left the buyer system?

Look for evidence such as:

- PO status
- Output/transmission status
- Integration transaction ID
- Payload
- Gateway status
- Business Network document status
- ERP/interface log

**Principle:** Do not assume transmission just because the PO exists.

---

# PART C — INVOICE / RECONCILIATION

## 26. What invoice types should you know?

- PO-based invoice
- Non-PO invoice
- Credit memo
- Debit memo
- Service-related invoice
- Contract-related invoice where applicable

---

## 27. What is invoice reconciliation?

**Answer:** Evaluation of invoice information against purchasing/receiving information and configured business rules/tolerances to determine whether the invoice can proceed or requires exception handling.

---

## 28. What is 2-way matching?

Conceptually:

```text
PO ↔ Invoice
```

---

## 29. What is 3-way matching?

Conceptually:

```text
        PO
       /  \
      /    \
Invoice ↔ Receipt
```

The exact matching behavior depends on the configured process and system.

---

## 30. PO = 100, GR = 80, Invoice = 100. What do you investigate?

**Answer:**

- Receipt quantity
- Invoice quantity
- PO quantity
- Tolerance rules
- Partial delivery status
- Whether remaining receipt is expected
- Supplier invoice correctness
- Exception workflow

Do not automatically call it an integration problem.

---

## 31. PO price = ₹1,000, invoice price = ₹1,100. What do you check?

Check:

1. PO price
2. Invoice line price
3. Currency
4. Quantity
5. Tax
6. Freight
7. Discounts
8. Contract conditions if applicable
9. Price tolerance
10. Any transformation/mapping issue

---

## 32. What is a tolerance?

**Answer:** A configured allowance for acceptable variance, such as a quantity or price difference.

---

## 33. Invoice is blocked. What is your approach?

```text
Invoice
  ↓
Status
  ↓
Exact Exception
  ↓
PO
  ↓
Receipt
  ↓
Price / Quantity / Tax
  ↓
Tolerance
  ↓
Master Data
  ↓
Root Cause
  ↓
Correction
  ↓
Reconciliation / Reprocessing
```

---

## 34. Supplier says invoice was submitted but buyer cannot see it. What do you do?

Trace:

```text
Supplier Submission
      ↓
Business Network Validation
      ↓
Routing
      ↓
Buyer Application
      ↓
Integration
      ↓
ERP
```

Capture the invoice/document identifier first.

---

## 35. How do you distinguish supplier-side vs network-side vs ERP-side failure?

Ask:

```text
Was it submitted?
       ↓
Was it accepted?
       ↓
Was it routed?
       ↓
Did buyer application receive it?
       ↓
Was ERP document created?
       ↓
Did ERP processing succeed?
```

The first failed step narrows the investigation.

---

# PART D — SAP MM / ERP

## 36. What is SAP MM?

**Answer:** SAP MM is the ERP functional area covering procurement/material-related processes, purchasing, inventory, goods movements, and invoice verification-related processing depending on the SAP ERP/S/4HANA solution and configuration.

---

## 37. Is SAP MM a separate system from ECC or S/4HANA?

**Answer:** No. SAP MM is a functional area within SAP ERP / SAP S/4HANA.

```text
SAP ECC / S/4HANA
        │
        ├── MM
        ├── FI
        ├── SD
        └── Other ERP areas
```

---

## 38. Explain the SAP MM organizational structure.

A useful conceptual distinction:

```text
Enterprise / Logistics

Client
  ↓
Company Code
  ↓
Plant
  ↓
Storage Location
```

Purchasing responsibility concepts:

```text
Purchasing Organization
        ↓
Purchasing responsibility / scope

Purchasing Group
        ↓
Buyer / purchasing responsibility
```

> Purchasing Group should not be described as a structural child of Purchasing Organization in the same sense as Storage Location under Plant.

---

## 39. What is a company code?

**Answer:** An organizational unit representing a legal/accounting entity for financial reporting purposes.

---

## 40. What is a plant?

**Answer:** An organizational unit used for functions such as procurement, inventory, production, or logistics depending on configuration.

---

## 41. What is a storage location?

**Answer:** An organizational subdivision of a plant used to identify where stock is stored.

---

## 42. What is a purchasing organization?

**Answer:** An organizational unit responsible for procurement activities and purchasing relationships.

---

## 43. What is a purchasing group?

**Answer:** A grouping used to represent purchasing agents or buyer responsibility.

---

## 44. Purchasing Organization vs Purchasing Group?

| Purchasing Organization | Purchasing Group |
|---|---|
| Procurement organizational responsibility | Buyer/team responsibility |
| Defines purchasing scope | Identifies purchasing agent/group |
| Organizational concept | Responsibility concept |

---

## 45. What is a material master?

**Answer:** Central material-related master data used by SAP processes. Depending on the process, it can contain information relevant to procurement, inventory, planning, valuation and other functions.

---

## 46. What is a Business Partner in S/4HANA?

**Answer:** Business Partner is the central master-data object used for managing business partners, including supplier/customer roles depending on the configuration.

---

## 47. What is a supplier master?

**Answer:** Supplier information used by procurement and related processes. In S/4HANA, supplier data is managed through the Business Partner approach with relevant supplier roles.

---

## 48. Explain PR → PO → GR → Invoice in SAP MM.

```text
PR
 ↓
Source / Purchasing
 ↓
PO
 ↓
Goods Receipt
 ↓
Invoice Verification
 ↓
Accounting / Payment
```

The exact document creation and integration path depends on architecture and configuration.

---

## 49. What is MIGO?

**Answer:** MIGO is a commonly used SAP GUI transaction for goods movements such as goods receipts and other inventory movements.

---

## 50. What is MIRO?

**Answer:** MIRO is a commonly used SAP GUI transaction for invoice verification in SAP ERP scenarios.

---

## 51. What is MM03?

**Answer:** MM03 is commonly used to display material master data.

---

## 52. What is MMBE?

**Answer:** MMBE is commonly used to display stock overview.

---

## 53. What is ME21N?

**Answer:** ME21N is commonly used to create a purchase order.

---

## 54. What is ME23N?

**Answer:** ME23N is commonly used to display a purchase order.

---

## 55. What is ME51N?

**Answer:** ME51N is commonly used to create a purchase requisition.

---

## 56. What is SLG1?

**Answer:** SLG1 displays SAP application logs.

**Interview warning:** Do not claim a specific application object/subobject unless you know the customer's configuration.

---

## 57. What is ST22?

**Answer:** ST22 is commonly used to analyze ABAP runtime errors/dumps.

---

## 58. What is SM37?

**Answer:** SM37 is commonly used to monitor background jobs.

---

## 59. What is SM58?

**Answer:** SM58 is commonly used to monitor transactional RFC entries in relevant SAP landscapes.

---

## 60. What is SRT_MONI?

**Answer:** SRT_MONI is used in relevant SAP environments to monitor web-service messages.

---

## 61. What is WE02 / WE05?

**Answer:** Common transactions used to display IDoc information.

---

## 62. What is BD87?

**Answer:** BD87 is commonly used for IDoc monitoring/reprocessing in relevant scenarios.

---

# PART E — SAP MM PRACTICAL SCENARIOS

## 63. PO exists in Ariba but not in ECC/S/4HANA. What do you check?

```text
Ariba PO
   ↓
Approved?
   ↓
Output generated?
   ↓
Integration transaction?
   ↓
Payload created?
   ↓
Gateway accepted?
   ↓
Cloud Connector?
   ↓
ECC interface?
   ↓
ERP application validation?
```

Then check:

- Document ID
- Integration status
- Payload
- Mapping
- Endpoint
- Authentication
- Cloud Connector
- IDoc/proxy/API status
- ERP application log
- Master data
- Business validation

---

## 64. PO reached ERP interface but ERP rejected it. Is CIG broken?

**Answer:** Not necessarily.

If the message successfully reached the ERP interface and the ERP rejected it because of a business rule or master-data problem, the root cause may be backend processing rather than the gateway.

---

## 65. Plant does not exist in ERP. What happens?

Possible flow:

```text
Ariba
  ↓
Payload contains Plant 1999
  ↓
Mapping
  ↓
ERP
  ↓
Plant validation
  ↓
ERROR
```

Investigate:

- Source value
- Mapping
- Value mapping
- Target plant
- ERP master data
- Configuration

---

## 66. Material number is invalid. How do you troubleshoot?

1. Identify material value in source.
2. Inspect payload.
3. Check transformation/mapping.
4. Check target material master.
5. Check plant/material extension where relevant.
6. Verify whether the correct identifier was sent.
7. Correct the appropriate source/mapping/master data.
8. Reprocess safely.

---

## 67. Cost center is rejected by ERP. What do you check?

Check:

- Cost center value
- Company code
- Validity date
- Source data
- Mapping
- Target master data
- Accounting configuration
- Whether the cost center is valid for the relevant organizational context

---

## 68. GL account is invalid. Is it an integration problem?

**Answer:** It may be a backend business/master-data/configuration issue even if the transaction arrived through integration successfully.

First identify where the value became invalid.

---

## 69. PO reaches ERP but fails during document creation. What is your troubleshooting sequence?

```text
Interface Received
       ↓
Payload Valid?
       ↓
Mapping Correct?
       ↓
Mandatory Fields?
       ↓
Master Data?
       ↓
Organizational Data?
       ↓
ERP Business Validation?
       ↓
Application Log / Error
       ↓
Root Cause
```

---

## 70. Goods Receipt is not reflected back in the procurement process. What do you investigate?

Check:

- GR actually posted?
- Material document created?
- Correct PO/item?
- Quantity?
- Movement type?
- Integration/output status?
- Business Network transaction?
- Mapping?
- Application logs?
- Any synchronization delay?

---

# PART F — CLOUD CONNECTOR

## 71. What is SAP Cloud Connector?

**Answer:** SAP Cloud Connector provides controlled connectivity between SAP cloud applications/platform services and selected on-premise systems.

SAP documentation describes it as a secure link for cloud-to-on-premise communication and uses access-control configuration to specify which backend systems/resources are reachable. citeturn0search0turn0search2

---

## 72. Why is Cloud Connector used?

**Answer:** It provides a controlled connectivity path between cloud services and on-premise systems without simply exposing the backend directly to the public internet.

---

## 73. Explain Cloud Connector at a high level.

```text
SAP Cloud / BTP
       │
       │ Secure Tunnel
       ▼
SAP Cloud Connector
       │
       │ Controlled Access
       ▼
On-Premise SAP ERP / S/4HANA
```

---

## 74. What is the difference between virtual host and internal host?

**Answer:**

- **Internal host:** Actual backend host reachable inside the customer network.
- **Virtual host:** Logical host exposed to the cloud side through Cloud Connector mapping.

The virtual host can hide the actual internal hostname.

---

## 75. What is access control in Cloud Connector?

**Answer:** Access control determines which backend systems and resource paths cloud applications are permitted to access.

SAP documentation shows Cloud Connector configuration using **Cloud To On-Premise**, system mappings, and resources with defined URL paths/access policies. citeturn0search1turn0search3

---

## 76. Why can Cloud Connector show a green connection while the transaction still fails?

Because tunnel connectivity does not prove that the business request is valid.

Possible later failures:

```text
Cloud Connector Connected
        ↓
Request Allowed?
        ↓
Correct Resource?
        ↓
Correct Host/Port?
        ↓
Authentication?
        ↓
ERP Endpoint?
        ↓
ERP Application?
        ↓
Business Validation?
```

---

## 77. Cloud Connector is connected but ERP is unreachable. What do you check?

Check:

1. Cloud Connector status
2. Subaccount association
3. System mapping
4. Internal host
5. Internal port
6. Virtual host/port
7. Protocol
8. Access-control resource
9. Resource path
10. Firewall/network
11. ERP service availability
12. Certificate/trust where applicable

SAP's current documentation emphasizes that merely establishing the tunnel does not automatically permit requests; backend resources must be explicitly allowed through access control. citeturn0search2

---

## 78. Cloud Connector system mapping is correct, but request returns 403/forbidden. What do you investigate?

Likely areas:

- Resource not allowed
- Wrong path
- Access policy
- Authorization
- Authentication/principal setup
- Application-level authorization
- Endpoint permissions

Do not immediately conclude network failure.

---

## 79. Cloud Connector system mapping is correct, but request returns 404. What do you investigate?

Check:

- URL path
- Virtual host
- Backend endpoint
- Service availability
- Resource mapping
- Application route
- Whether the requested service actually exists

---

## 80. Cloud Connector tunnel is down. What is your first investigation?

```text
Cloud Connector
      ↓
Subaccount connection
      ↓
Internet / proxy
      ↓
Firewall
      ↓
Cloud Connector service
      ↓
Credentials / certificates
      ↓
System resources
```

Separate **tunnel failure** from **backend application failure**.

---

## 81. What is principal propagation?

**Answer:** A mechanism that can allow the identity of a cloud user/request to be propagated toward an on-premise backend where the architecture and trust configuration support it.

Do not claim it is required for every Ariba integration scenario.

---

## 82. What is the difference between connectivity and authorization?

```text
Connectivity
= Can I reach the target?

Authorization
= Am I allowed to perform the operation?
```

A system can be reachable while the request is unauthorized.

---

# PART G — MANAGED GATEWAY / CIG

## 83. What is CIG?

**Answer:** CIG is the commonly used historical name for Cloud Integration Gateway. Current SAP terminology is **SAP Integration Suite, managed gateway for spend management and SAP Business Network**.

---

## 84. Why is Managed Gateway used?

**Answer:** It supports integration between SAP procurement/spend solutions, SAP Business Network, and backend ERP systems for supported processes and document exchange.

SAP documentation describes ERP/S/4HANA integration components including the managed gateway and Cloud Connector. citeturn0search0

---

## 85. Explain a typical ERP → Business Network flow.

```text
SAP ERP / S/4HANA
       ↓
ERP Add-On / Integration Components
       ↓
Integration / Managed Gateway
       ↓
SAP Business Network
       ↓
Supplier
```

The exact path depends on the configured integration architecture.

---

## 86. Explain an inbound Business Network → ERP flow.

```text
Supplier
   ↓
SAP Business Network
   ↓
Managed Gateway
   ↓
Integration / Middleware
   ↓
Cloud Connector
   ↓
SAP ERP / S/4HANA
   ↓
Business Processing
```

SAP's current installation documentation describes inbound transactions flowing through Managed Gateway and integration services and then through Cloud Connector to ERP/S/4HANA in applicable architectures. citeturn0search7

---

## 87. What is endpoint configuration?

**Answer:** Endpoint configuration identifies where and how a transaction should be routed. Exact endpoint details depend on the integration scenario.

---

## 88. What is mapping?

**Answer:** Mapping transforms source fields and values into the structure/value expected by the target.

```text
Source
  ↓
Transformation
  ↓
Mapping
  ↓
Target Payload
```

---

## 89. What is value mapping?

**Answer:** Translating one system's value into another system's expected value.

Example:

```text
Ariba Commodity = IT_SERVICES
          ↓
ERP Value       = 004500
```

The actual mapping depends on customer configuration.

---

## 90. What is a payload?

**Answer:** The actual data/message sent between systems.

When troubleshooting, inspect:

- Header
- Document ID
- Sender
- Receiver
- Line items
- Quantity
- Currency
- Organization
- Supplier
- Accounting data
- Error response

---

# PART H — cXML / DOCUMENT-LEVEL INTERVIEW

## 91. What is cXML?

**Answer:** cXML is an XML-based standard used for supported procurement/business-document exchanges.

---

## 92. What is OrderRequest?

**Answer:** A cXML document representing an order transaction in supported scenarios.

```text
Buyer
 ↓
OrderRequest
 ↓
Business Network
 ↓
Supplier
```

---

## 93. What is ConfirmationRequest?

**Answer:** A cXML document used in supported scenarios to communicate supplier confirmation information.

---

## 94. What is ShipNoticeRequest?

**Answer:** A cXML document used to communicate shipment/ASN information in supported scenarios.

---

## 95. What is InvoiceDetailRequest?

**Answer:** A cXML document used to represent invoice details in supported scenarios.

SAP documentation lists `InvoiceDetailRequest` among supported cXML document types. citeturn0search17

---

## 96. What is PunchOutSetupRequest?

**Answer:** A cXML message used to initiate supported PunchOut sessions between the procurement application and supplier site.

---

## 97. cXML payload looks valid XML but transaction fails. Why?

Valid XML syntax does not guarantee valid business processing.

Possible reasons:

- Invalid business value
- Missing mandatory field
- Wrong identifier
- Wrong supplier
- Mapping issue
- Invalid organizational data
- Invalid master data
- Authentication/authorization
- Business rule rejection

---

## 98. How do you read a failed cXML payload?

Start with:

```text
Document Type
      ↓
Payload ID / Transaction ID
      ↓
Sender
      ↓
Receiver
      ↓
Document Number
      ↓
Header
      ↓
Line Items
      ↓
Quantity / Price
      ↓
Currency
      ↓
Organization
      ↓
Supplier
      ↓
Accounting
      ↓
Response / Error
```

---

# PART I — APIs / HTTP

## 99. API vs cXML?

**Answer:**

- API = programmatic interface.
- cXML = business document/message format.

They are not the same concept.

---

## 100. What HTTP methods should you know?

```text
GET     → Retrieve
POST    → Create / submit
PUT     → Replace
PATCH   → Partial update
DELETE  → Delete
```

---

## 101. What does HTTP 401 mean?

**Answer:** Authentication is missing/invalid or not accepted.

---

## 102. What does HTTP 403 mean?

**Answer:** The request is understood but not authorized to perform the requested operation.

---

## 103. What does HTTP 404 mean?

**Answer:** The requested resource/endpoint could not be found.

---

## 104. What does HTTP 409 mean?

**Answer:** Conflict. The exact cause depends on the API.

---

## 105. What does HTTP 429 mean?

**Answer:** Too many requests/rate limiting.

---

## 106. What does HTTP 500 mean?

**Answer:** Server-side error. Investigate server/application logs and response details.

---

## 107. How do you troubleshoot an API failure?

```text
Endpoint
  ↓
DNS / Connectivity
  ↓
Authentication
  ↓
Authorization
  ↓
Headers
  ↓
Parameters
  ↓
Payload
  ↓
HTTP Response
  ↓
Application Logs
```

---

# PART J — SAP INTEGRATION MONITORING

## 108. What is SLG1 used for?

**Answer:** SAP application log display.

---

## 109. What is ST22 used for?

**Answer:** ABAP runtime error/dump analysis.

---

## 110. What is SM37 used for?

**Answer:** Background job monitoring.

---

## 111. What is SM58 used for?

**Answer:** Monitoring transactional RFC entries in applicable SAP scenarios.

---

## 112. What is SM59?

**Answer:** RFC destination configuration and testing in SAP systems.

---

## 113. What are WE02 / WE05?

**Answer:** IDoc display/monitoring transactions.

---

## 114. What is BD87?

**Answer:** IDoc monitoring/reprocessing transaction in applicable scenarios.

---

## 115. What is SRT_MONI?

**Answer:** Web-service message monitoring in applicable SAP environments.

---

## 116. What is SM21?

**Answer:** SAP system log monitoring.

---

## 117. Why should you not blindly list transactions in an interview?

Because the correct monitoring tool depends on the integration technology.

A good answer is:

> "I first identify whether the failure is in application processing, IDoc, web service, RFC, middleware, Cloud Connector, or Business Network. Then I use the monitoring tool relevant to that layer."

---

# PART K — MASTER DATA / INTEGRATION

## 118. Why can technically successful messages still fail?

Because transport success does not equal business-processing success.

```text
Message Delivered
      ↓
ERP Receives
      ↓
Business Validation
      ↓
FAILURE
```

Examples:

- Invalid plant
- Invalid company code
- Invalid material
- Invalid supplier
- Invalid cost center
- Invalid GL
- Missing purchasing data

---

## 119. Plant is missing in ERP but exists in Ariba. What do you check?

Check:

1. Source value
2. Payload
3. Mapping
4. Target ERP plant
5. Master data
6. Organizational assignment
7. Configuration
8. Reprocessing requirement

---

## 120. Supplier ID is different between Ariba and ERP. What do you investigate?

```text
Ariba Supplier ID
       ↓
Mapping / Cross Reference
       ↓
ERP Supplier / Business Partner
```

Check:

- Source identifier
- Mapping
- Supplier relationship
- ERP Business Partner/supplier
- Target identifier
- Integration configuration

---

# PART L — REAL-WORLD SCENARIOS

## 121. Scenario: PO not reaching supplier

**Interviewer:** "A PO was created two hours ago and the supplier still cannot see it. What do you do?"

**Answer structure:**

```text
1. Confirm PO
2. Confirm approval/release
3. Confirm transmission
4. Capture transaction/document ID
5. Check Business Network status
6. Check supplier relationship
7. Check routing
8. Check payload
9. Check integration/gateway
10. Check endpoint
11. Check ERP/application logs if relevant
12. Identify root cause
13. Correct
14. Reprocess
15. Validate supplier receipt
```

---

## 122. Scenario: PO not reaching ERP

**Interviewer:** "The PO exists in Ariba but does not exist in S/4HANA. What do you check?"

**Answer:**

```text
Ariba PO
   ↓
Integration Transaction?
   ↓
Payload?
   ↓
Mapping?
   ↓
Gateway?
   ↓
Cloud Connector?
   ↓
ERP Interface?
   ↓
ERP Application?
```

Do not start by blaming CIG.

---

## 123. Scenario: Cloud Connector is green but transaction fails

**Answer:**

> "A green Cloud Connector connection proves the connector/subaccount connection is established, but it does not prove that the requested resource, endpoint, authorization, or backend application processing is successful. I would inspect access control, resource path, endpoint, authentication, backend availability and the application error."

SAP documentation explicitly separates the tunnel connection from access-control/resource permissions. citeturn0search2

---

## 124. Scenario: 403 from backend

Investigate:

```text
Authentication
      ↓
Authorization
      ↓
Cloud Connector Access Control
      ↓
Resource Path
      ↓
Backend Authorization
```

---

## 125. Scenario: 404 from backend

Investigate:

- URL
- Virtual host
- Resource path
- Backend service
- Endpoint
- Application route

---

## 126. Scenario: 500 from backend

Investigate:

- Application error
- Backend logs
- ABAP dump
- Application log
- Input payload
- Business validation
- Recent deployment/configuration change

---

## 127. Scenario: Invalid material

**Answer:**

> "I would identify the material value at source and in the payload, determine whether it was transformed, then validate the material in the target ERP and relevant organizational views. I would correct the source/mapping/master-data issue at the correct layer rather than manually changing the transaction without understanding the root cause."

---

## 128. Scenario: Invalid cost center

Check:

- Cost center
- Company code
- Validity
- Source payload
- Mapping
- ERP master data
- Accounting configuration

---

## 129. Scenario: Duplicate PO

Investigate:

```text
Original transaction ID
        ↓
Retry
        ↓
Reprocessing
        ↓
Second submission
        ↓
Duplicate document
```

Questions:

- Was the original actually successful?
- Did timeout occur after successful processing?
- Was the transaction retried?
- Is there an idempotency/reference mechanism?
- Did ERP create the document before response was lost?

---

## 130. Scenario: Integration timed out but ERP document exists

**Strong answer:**

> "I would not immediately retry. First I would confirm whether the ERP document was created successfully. A timeout does not prove that backend processing failed; the request may have completed but the response may not have returned. I would identify the transaction/document ID and determine the actual business state before reprocessing."

This is a critical production-support principle.

---

## 131. Scenario: Supplier receives the PO twice

Investigate:

- Duplicate source event
- Retry
- Middleware retry
- Network retry
- Duplicate integration transaction
- Supplier routing
- Document identifiers
- Whether first transaction was acknowledged

---

## 132. Scenario: Invoice submitted twice

Check:

- Invoice number
- Supplier
- PO
- Network transaction
- Duplicate validation
- Retry history
- Integration logs
- ERP invoice document
- Whether one submission was actually accepted

---

## 133. Scenario: ASN received but goods receipt is missing

Possible investigation:

```text
ASN
 ↓
Business Network
 ↓
ERP / Integration
 ↓
Inbound processing
 ↓
PO/item
 ↓
Goods receipt process
```

Check whether ASN receipt itself should create a GR in the customer's design. Do not assume ASN automatically means GR.

---

## 134. Scenario: GR exists in ERP but Ariba status is not updated

Check:

- GR document
- Material document
- Integration/output
- Business Network transaction
- Mapping
- Payload
- Endpoint
- Status processing
- Application logs

---

## 135. Scenario: Invoice is valid XML but rejected by ERP

Possible reasons:

- Invalid supplier
- Invalid PO
- Invalid tax
- Invalid currency
- Invalid accounting
- Missing master data
- Tolerance/business rule
- Mapping
- Backend validation

---

# PART M — CLOUD CONNECTOR DEEP-DIVE

## 136. What are the major Cloud Connector configuration concepts?

Know:

- BTP subaccount association
- Cloud To On-Premise
- System mapping
- Internal host
- Internal port
- Virtual host
- Virtual port
- Protocol
- Principal type
- Access control
- Resources
- Resource paths
- Connectivity status

SAP documentation uses system mappings and resource-level access control as core configuration concepts. citeturn0search1turn0search5

---

## 137. What is a resource in Cloud Connector?

**Answer:** A resource defines a URL/path that the connected cloud application is allowed to access on the mapped backend.

---

## 138. Why is path-level access important?

Because the Cloud Connector does not simply expose the entire backend automatically. Access can be limited to specific resources/path patterns.

---

## 139. Cloud Connector is up but resource is disabled. What happens?

The cloud request can fail because the requested backend resource is not permitted.

---

## 140. Internal host works from the corporate network but Cloud Connector request fails. What do you check?

Separate:

```text
Corporate Network Reachability
        ≠
Cloud Connector Reachability
        ≠
Resource Authorization
        ≠
Application Authorization
```

Then check:

- Internal host/port
- Connector host
- Firewall
- Protocol
- System mapping
- Resource
- Backend service

---

# PART N — SAP MM DEEP-DIVE

## 141. What is the difference between PR and PO in SAP MM?

**Answer:** PR is an internal requirement/request; PO is the purchasing document issued to a supplier.

---

## 142. What is the role of a plant in procurement?

A plant can represent a location/organizational unit involved in procurement and logistics. The exact use depends on configuration and process.

---

## 143. What is the role of purchasing organization?

It represents the procurement organization/responsibility under which purchasing activities are performed.

---

## 144. What is the role of purchasing group?

It identifies the buyer or purchasing responsibility/group handling procurement activities.

---

## 145. What is a goods movement?

**Answer:** A transaction that changes inventory or records a logistics movement, such as receipt, issue, transfer, or reversal.

---

## 146. What is movement type 101?

Commonly associated with a goods receipt for a purchase order.

---

## 147. What is movement type 102?

Commonly associated with reversal of a 101 goods receipt.

---

## 148. What is movement type 122?

Commonly associated with return delivery to vendor in relevant SAP processes.

> Exact usage depends on configuration/process.

---

## 149. What is movement type 201?

Commonly associated with goods issue to a cost center.

---

## 150. What is movement type 261?

Commonly associated with goods issue to a production order.

---

## 151. What is movement type 301?

Commonly associated with plant-to-plant transfer posting.

---

## 152. What is movement type 311?

Commonly associated with storage-location-to-storage-location transfer posting.

---

## 153. What happens when a GR is posted?

At a high level:

```text
PO
 ↓
Goods Receipt
 ↓
Material Document
 ↓
Stock Update
 ↓
Relevant Accounting / Valuation Effects
```

Exact accounting impact depends on material valuation and configuration.

---

## 154. What happens during invoice verification?

Conceptually:

```text
Supplier Invoice
      ↓
PO / Receipt / Rules
      ↓
Invoice Verification
      ↓
Accounting Document
      ↓
Payment Process
```

---

## 155. What is 3-way matching in SAP MM?

Compare:

```text
Purchase Order
      ↕
Goods Receipt
      ↕
Invoice
```

The exact tolerance and matching behavior depends on configuration.

---

# PART O — INTERVIEWER CROSS-QUESTIONS

## 156. You said you know CIG. What exactly did you do?

Good answer:

> "My exposure was primarily in troubleshooting/support. I worked with transaction status, payload/error analysis and integration-related issues. I understand the architecture and troubleshooting flow, but I would distinguish that from hands-on configuration or development unless I actually performed those activities."

---

## 157. You said you know Cloud Connector. Did you configure it?

If you did not:

> "I understand the architecture and troubleshooting concepts, including system mapping, virtual/internal host concepts and access control. I would not claim that I personally configured production Cloud Connector unless I actually did."

This is stronger than pretending.

---

## 158. You said you know SAP MM. Did you work directly in MM?

Separate:

```text
Hands-on
Conceptual
Troubleshooting Exposure
Integration Exposure
```

Example:

> "My primary role was Ariba/P2P support. I worked with ERP-side concepts and integration issues, and I understand MM procurement flows, documents and relevant troubleshooting. I would not present myself as an MM functional consultant if my actual role was Ariba support."

---

## 159. Did you implement SAP Ariba?

If you supported rather than implemented:

> "My experience is stronger in production support and troubleshooting than in owning a complete implementation lifecycle. I understand implementation concepts such as requirement gathering, configuration, integration, testing and go-live, but I distinguish that conceptual knowledge from direct implementation ownership."

---

## 160. What is the most difficult Ariba issue you handled?

Use:

```text
Situation
   ↓
Business Impact
   ↓
Investigation
   ↓
Technical Evidence
   ↓
Root Cause
   ↓
Resolution
   ↓
Validation
   ↓
Prevention
```

Never invent a production incident.

---

# PART P — 20 RAPID-FIRE SCENARIOS

## 161. PO exists, supplier does not see it.

**Answer:** Check release → transmission → Business Network → supplier relationship → routing → integration → payload.

## 162. PO exists in Ariba, not ERP.

**Answer:** Trace outbound/inbound integration → gateway → Cloud Connector → ERP interface → application validation.

## 163. ERP returns invalid plant.

**Answer:** Check source plant → mapping → target plant master/configuration.

## 164. ERP returns invalid supplier.

**Answer:** Check supplier identifier → mapping → Business Partner/supplier master → purchasing data.

## 165. ERP returns invalid cost center.

**Answer:** Check company code, validity, source value, mapping, and target master data.

## 166. Invoice quantity exceeds receipt.

**Answer:** Check PO, GR, invoice, tolerance and business exception.

## 167. Invoice price differs from PO.

**Answer:** Check price, currency, tax, freight, discount, contract and tolerance.

## 168. Cloud Connector green, request fails.

**Answer:** Check access control/resource, endpoint, authentication, backend service and application error.

## 169. Cloud Connector down.

**Answer:** Check subaccount connection, network/proxy/firewall, connector service and credentials/certificates.

## 170. HTTP 401.

**Answer:** Investigate authentication.

## 171. HTTP 403.

**Answer:** Investigate authorization/access control.

## 172. HTTP 404.

**Answer:** Investigate endpoint/resource/path.

## 173. HTTP 500.

**Answer:** Investigate server/application/backend logs.

## 174. HTTP 429.

**Answer:** Investigate rate limiting/throttling and retry behavior.

## 175. XML valid but business transaction fails.

**Answer:** XML syntax is valid; business validation can still fail.

## 176. Timeout occurred, but document exists.

**Answer:** Do not blindly retry; determine actual business state first.

## 177. Duplicate document after retry.

**Answer:** Investigate whether original processing succeeded before the retry.

## 178. ASN exists but GR is missing.

**Answer:** Check whether the process is designed to create/trigger GR, then trace inbound processing and ERP posting.

## 179. GR exists but downstream status is missing.

**Answer:** Trace GR/output → integration → Business Network/application → mapping/status processing.

## 180. Supplier cannot submit invoice.

**Answer:** Check supplier enablement, transaction channel, validation error, network relationship and supported document/channel.

---

# PART Q — CONSULTING / IMPLEMENTATION

## 181. How do you gather requirements?

```text
Business Goal
     ↓
Current Process
     ↓
Pain Point
     ↓
Business Rules
     ↓
Users / Volume
     ↓
Systems
     ↓
Integration
     ↓
Standard Capability
     ↓
Gap
     ↓
Solution
```

---

## 182. What is fit-to-standard?

**Answer:** Evaluate standard SAP capability first before deciding that customization or extension is required.

---

## 183. What is gap analysis?

**Answer:** Compare required business capability with standard product capability and identify differences requiring configuration, process change, integration, extension, or other solution design.

---

## 184. Client wants customization for every requirement. What do you do?

**Answer:**

1. Clarify the actual business outcome.
2. Check standard capability.
3. Check configuration.
4. Consider process redesign.
5. Evaluate extension/integration.
6. Discuss cost and maintenance.
7. Consider upgrade impact.
8. Recommend a sustainable option.

---

## 185. How do you explain a technical issue to a business user?

Use:

```text
What happened?
     ↓
Business Impact
     ↓
Why it happened
     ↓
What we are doing
     ↓
Expected resolution
     ↓
Prevention
```

Avoid unnecessary technical jargon.

---

# PART R — PRODUCTION SUPPORT / RCA

## 186. What is your incident approach?

```text
Incident
  ↓
Business Impact
  ↓
Document / Transaction ID
  ↓
Direction
  ↓
Failure Layer
  ↓
Evidence
  ↓
Root Cause
  ↓
Fix
  ↓
Validation
  ↓
RCA
```

---

## 187. Incident vs Problem vs Change?

| Term | Meaning |
|---|---|
| Incident | Service failure/impact |
| Problem | Underlying cause of one or more incidents |
| Change | Controlled system modification |

---

## 188. How do you prioritize incidents?

Consider:

- Business impact
- Number of users
- Financial impact
- Payment impact
- Supplier impact
- Production/non-production
- Workaround
- SLA

---

## 189. What belongs in an RCA?

```text
Problem Statement
Business Impact
Timeline
Technical Evidence
Root Cause
Contributing Factors
Resolution
Validation
Preventive Action
```

---

## 190. What makes a good support engineer?

An interview-safe answer:

> "I try to isolate the failure layer before changing anything. I use transaction/document identifiers, logs and payload evidence, distinguish symptoms from root causes, communicate the business impact clearly, and validate the final business result after resolution."

---

# PART S — ADVANCED PRACTICAL QUESTIONS

## 191. Why is "CIG is down" a weak troubleshooting statement?

Because the failure could be:

- Ariba application
- Business Network
- Supplier relationship
- Payload
- Mapping
- Gateway
- Cloud Connector
- ERP interface
- ERP application
- Master data
- Business configuration

Always identify evidence first.

---

## 192. What is the difference between technical success and business success?

```text
Technical Success
= Message transported

Business Success
= Transaction processed correctly
```

Example:

```text
Message Delivered
       ↓
ERP Received
       ↓
Invalid Plant
       ↓
Business Failure
```

---

## 193. Where should you fix bad master data?

At the correct ownership layer.

Do not permanently "fix" the payload manually if the real source/master data remains incorrect.

---

## 194. When should you reprocess a failed transaction?

Only after understanding:

1. Why it failed
2. Whether the original transaction partially succeeded
3. Whether retry can create duplicates
4. Whether the root cause is fixed
5. Whether the business state is safe to retry

---

## 195. Why can retry make an incident worse?

Because a timeout may hide successful processing.

```text
Request
  ↓
ERP Processes Successfully
  ↓
Response Lost / Timeout
  ↓
Engineer Retries
  ↓
Duplicate Transaction
```

---

## 196. How do you investigate a transaction with no obvious error?

Build the trace manually:

```text
Business Document ID
        ↓
Source Status
        ↓
Transmission ID
        ↓
Payload
        ↓
Network Status
        ↓
Integration Status
        ↓
ERP Document
        ↓
ERP Log
```

Find the first point where expected evidence disappears.

---

## 197. What is the difference between failure point and root cause?

Example:

```text
Failure Point:
ERP rejects Plant 1999

Root Cause:
Source/mapping/master-data configuration produced an invalid plant
```

The visible failure and underlying cause can be different.

---

## 198. How do you handle an escalation where another team says "Ariba is broken"?

Answer with evidence:

> "I would avoid assuming ownership from the symptom. I would identify the transaction ID, determine the last successful layer, capture the exact error and then identify whether the issue is application, network, integration, master data or backend processing."

---

## 199. How do you prove an integration issue?

Use evidence such as:

- Transaction ID
- Timestamp
- Payload
- HTTP response
- Gateway status
- Business Network status
- Cloud Connector status
- ERP log
- IDoc/web-service status
- Exact error

---

## 200. What is your strongest troubleshooting principle?

> **Trace the transaction from business document to technical message to backend processing, and identify the first failed layer with evidence.**

---

# PART T — INTERVIEWER TRAPS

## 201. "Is SAP MM the backend?"

**Better answer:**

> "SAP MM is an ERP functional area. In an Ariba landscape, ECC or S/4HANA can act as the ERP backend, and MM handles relevant procurement/material processes within that ERP system."

---

## 202. "Is Cloud Connector middleware?"

**Better answer:**

> "I would distinguish connectivity from business transformation. Cloud Connector provides controlled cloud-to-on-premise connectivity. It is not the same thing as a business mapping/transformation layer."

---

## 203. "If Cloud Connector is green, is integration working?"

**Answer:** No. It proves connectivity at that layer, not complete business transaction success.

---

## 204. "If XML is valid, is the transaction valid?"

**Answer:** No. XML syntax validity is different from business validation.

---

## 205. "If the PO exists, was it sent?"

**Answer:** Not necessarily. Verify transmission/output/integration evidence.

---

## 206. "If the ERP received the message, is integration successful?"

**Answer:** Transport may be successful, but ERP business processing can still fail.

---

## 207. "Should you always retry failed messages?"

**Answer:** No. First determine whether the original transaction partially or fully succeeded and whether retry can create duplicates.

---

## 208. "Can an ASN automatically mean goods receipt?"

**Answer:** Not universally. It depends on the configured business process and integration design.

---

## 209. "Is every invoice 3-way matched?"

**Answer:** No. Matching behavior depends on the transaction type and configured process/rules.

---

## 210. "Can you explain every SAP MM transaction?"

**Answer:** Do not bluff. Explain the transactions you know and the monitoring approach you actually understand.

---

# PART U — PERSONAL EXPERIENCE QUESTIONS

## 211. Tell me about your SAP Ariba experience.

Use:

```text
Current / Previous Role
       ↓
Ariba Area
       ↓
P2P Exposure
       ↓
Support Responsibilities
       ↓
Integration Exposure
       ↓
Troubleshooting
       ↓
RCA
       ↓
Current Learning
```

---

## 212. Did you work on implementation?

If your experience is support-focused:

> "My primary exposure has been production/support rather than owning a complete implementation. I understand the implementation lifecycle and the technical/functional dependencies, but I distinguish that conceptual understanding from direct implementation ownership."

---

## 213. Did you configure CIG?

If you did not personally configure it:

> "I have troubleshooting and architectural understanding of Managed Gateway/CIG, including transaction flow, payloads and integration failure analysis. I would not claim hands-on production configuration unless I actually performed it."

---

## 214. Did you configure Cloud Connector?

If not:

> "I understand Cloud Connector architecture, system mapping, virtual/internal host concepts, access control and troubleshooting. I would distinguish that knowledge from direct configuration experience."

---

## 215. Did you work on SAP MM?

If your exposure is primarily Ariba:

> "My primary area is SAP Ariba/P2P support. I have ERP/MM process and integration exposure, including procurement documents, goods movement concepts and troubleshooting, but I would not represent myself as an SAP MM functional consultant unless that was my actual role."

---

## 216. What was your most difficult ticket?

Answer with:

```text
Situation
Business Impact
What You Checked
Evidence
Root Cause
Action
Validation
Learning
```

---

## 217. What did you personally do vs what did another team do?

This is a very important interview distinction.

Use:

```text
I personally:
- Investigated
- Analyzed
- Coordinated
- Validated

Another team:
- Performed configuration/development if applicable
```

Never convert "I coordinated with the integration team" into "I developed the integration."

---

# PART V — 25 MOCK INTERVIEW QUESTIONS

## 218. Explain an end-to-end Ariba P2P transaction technically.

## 219. What happens when a PO leaves Ariba?

## 220. How does it reach SAP Business Network?

## 221. How does it reach ERP?

## 222. Where does Cloud Connector fit?

## 223. What is the role of Managed Gateway?

## 224. What happens if Cloud Connector is unavailable?

## 225. What happens if the supplier relationship is inactive?

## 226. What happens if mapping is wrong?

## 227. What happens if plant is invalid?

## 228. What happens if supplier ID is wrong?

## 229. What happens if PO price and invoice price differ?

## 230. What happens if receipt is missing?

## 231. How do you troubleshoot a 401?

## 232. How do you troubleshoot a 403?

## 233. How do you troubleshoot a 404?

## 234. How do you troubleshoot a 500?

## 235. How do you troubleshoot a timeout?

## 236. How do you prevent duplicate processing?

## 237. Which SAP transactions do you know for integration support?

## 238. How do you troubleshoot an IDoc?

## 239. How do you troubleshoot an application log?

## 240. How do you explain a technical failure to a business stakeholder?

## 241. How do you write an RCA?

## 242. How do you decide whether to reprocess?

---

# PART W — MINI CASE STUDIES

## 243. Case: PO not visible to supplier

### Facts

```text
PO = 4500001234
Buyer says: Created
Supplier says: Not received
```

### Investigation

```text
PO Exists
   ↓
Released?
   ↓
Transmission?
   ↓
Network?
   ↓
Supplier Relationship?
   ↓
Routing?
   ↓
Payload?
   ↓
Integration?
```

### Interview expectation

Do not jump to a conclusion. Explain how you would isolate the failure.

---

## 244. Case: PO missing in S/4HANA

### Facts

```text
Ariba = PO exists
Business Network = transaction exists
S/4HANA = no PO
```

### Investigation

```text
Network
  ↓
Integration
  ↓
Cloud Connector
  ↓
ERP Interface
  ↓
ERP Application
```

The likely failure is downstream of Business Network, but you still need evidence.

---

## 245. Case: ERP rejects plant

### Facts

```text
Plant = 1999
ERP = Plant does not exist
```

### Investigation

```text
Source
 ↓
Payload
 ↓
Mapping
 ↓
ERP Master Data
 ↓
Configuration
```

---

## 246. Case: Invoice mismatch

```text
PO = 100 units
GR = 90 units
Invoice = 100 units
```

### Interview answer

> "I would classify this as a quantity variance first. I would verify whether 90 is the actual received quantity, whether 10 are expected later, what tolerance applies, and whether the invoice is correct. I would not call it an integration failure without evidence."

---

## 247. Case: Timeout + duplicate

```text
Request
 ↓
Timeout
 ↓
Engineer retries
 ↓
Duplicate
```

### Lesson

> **Timeout is not proof of failed processing.**

---

## 248. Case: Cloud Connector green + 403

### Investigation

```text
Connector
   ↓
System Mapping
   ↓
Resource
   ↓
Authentication
   ↓
Authorization
   ↓
Backend
```

---

## 249. Case: cXML valid + ERP rejects

### Investigation

```text
XML Syntax
     ↓
Business Document
     ↓
Mapping
     ↓
Master Data
     ↓
ERP Validation
```

Valid XML does not guarantee valid business data.

---

# PART X — 50 VERY SHORT RAPID-FIRE QUESTIONS

## 250. What is PR?

Internal purchase request.

## 251. What is PO?

Formal purchase order.

## 252. What is GR?

Goods receipt.

## 253. What is IR?

Invoice receipt/invoice verification context, depending on terminology.

## 254. What is ASN?

Advance Ship Notice.

## 255. What is OC?

Order Confirmation.

## 256. What is S2C?

Source-to-Contract.

## 257. What is P2O?

Procure-to-Order.

## 258. What is P2P?

Procure-to-Pay.

## 259. What is SLP?

Supplier Lifecycle and Performance.

## 260. What is Business Network?

Buyer-supplier collaboration network.

## 261. What is CIG?

Historical/common name for Cloud Integration Gateway.

## 262. Current CIG terminology?

SAP Integration Suite, managed gateway for spend management and SAP Business Network.

## 263. What is cXML?

XML-based business document format.

## 264. What is CIF?

Catalog Interchange Format.

## 265. What is Cloud Connector?

Controlled cloud-to-on-premise connectivity component.

## 266. What is mapping?

Field/value transformation between systems.

## 267. What is payload?

Actual message/data sent.

## 268. What is endpoint?

Destination/interface used for communication.

## 269. What is authentication?

Verifying identity.

## 270. What is authorization?

Checking permissions.

## 271. What is idempotency?

Safe repeat behavior without unintended duplicate business effect.

## 272. What is SLG1?

Application log display.

## 273. What is ST22?

ABAP dump analysis.

## 274. What is SM37?

Background job monitoring.

## 275. What is SM59?

RFC destination configuration/testing.

## 276. What is SM58?

Transactional RFC monitoring.

## 277. What is WE02?

IDoc display.

## 278. What is WE05?

IDoc display/monitoring.

## 279. What is BD87?

IDoc monitoring/reprocessing.

## 280. What is MIGO?

Goods movement transaction.

## 281. What is MIRO?

Invoice verification transaction.

## 282. What is ME21N?

Create PO.

## 283. What is ME23N?

Display PO.

## 284. What is ME51N?

Create PR.

## 285. What is MM03?

Display material.

## 286. What is MMBE?

Stock overview.

## 287. What is movement type 101?

Commonly GR for PO.

## 288. What is movement type 102?

Commonly reversal of 101.

## 289. What is movement type 122?

Commonly return delivery to vendor.

## 290. What is movement type 201?

Commonly goods issue to cost center.

## 291. What is movement type 261?

Commonly goods issue to production order.

## 292. What is movement type 301?

Commonly plant-to-plant transfer.

## 293. What is movement type 311?

Commonly storage-location transfer.

## 294. What is 401?

HTTP authentication-related? **Do not guess.** Context matters.

## 295. What is 403?

Forbidden / authorization-related.

## 296. What is 404?

Not found.

## 297. What is 500?

Server/application error.

## 298. What is 429?

Rate limiting.

## 299. What is RCA?

Root Cause Analysis.

---

# PART Y — FINAL 20 QUESTIONS TO PRACTICE OUT LOUD

## 300. Explain SAP Ariba architecture in 2 minutes.

## 301. Explain Ariba P2P in 2 minutes.

## 302. Explain SAP Business Network in 1 minute.

## 303. Explain Managed Gateway/CIG in 1 minute.

## 304. Explain Cloud Connector in 1 minute.

## 305. Explain SAP MM's role in an Ariba landscape.

## 306. Explain PR vs PO.

## 307. Explain PO → GR → Invoice.

## 308. Explain 2-way vs 3-way matching.

## 309. Explain a blocked invoice.

## 310. Explain PO not reaching supplier.

## 311. Explain PO not reaching ERP.

## 312. Explain invalid plant.

## 313. Explain invalid supplier.

## 314. Explain Cloud Connector green but transaction failed.

## 315. Explain HTTP 403.

## 316. Explain timeout + duplicate risk.

## 317. Explain cXML troubleshooting.

## 318. Explain your production incident approach.

## 319. Explain your actual SAP Ariba experience without exaggerating.

---

# FINAL INTERVIEW FRAMEWORK

When the interviewer gives you a problem, do not jump directly to the tool.

Think:

```text
BUSINESS
   ↓
DOCUMENT
   ↓
SYSTEM
   ↓
DIRECTION
   ↓
INTEGRATION LAYER
   ↓
PAYLOAD
   ↓
MASTER DATA
   ↓
BACKEND PROCESSING
   ↓
ERROR
   ↓
ROOT CAUSE
   ↓
FIX
   ↓
VALIDATION
```

The strongest practical answers usually demonstrate five things:

1. **You understand the business process.**
2. **You know where the document should travel.**
3. **You can isolate the failing technical layer.**
4. **You use evidence instead of assumptions.**
5. **You know the difference between your actual hands-on experience and conceptual knowledge.**

---

# Official SAP References

Use official SAP documentation for release-specific behavior and configuration.

- [SAP Help Portal](https://help.sap.com/)
- [SAP Integration Suite, Managed Gateway for Spend Management and SAP Business Network](https://help.sap.com/docs/sisgw)
- [Managed Gateway software components](https://help.sap.com/docs/sisgw/sap-integration-suite-managed-gateway-for-spend-management-and-sap-business-network-overview-guide-for-erp-integration-for-suppliers/software-components)
- [Managed Gateway installation guide](https://help.sap.com/docs/sisgw/sap-ariba-cloud-integration-gateway-installation-guide)
- [Managed Gateway configuration guide](https://help.sap.com/docs/sisgw/sap-integration-suite-managed-gateway-for-spend-management-and-sap-business-network-configuration-guide-for-erp-integration-for-suppliers/sap-integration-suite-managed-gateway-for-spend-management-and-sap-business-network-configuration-guide-for-erp-integration-for-suppliers)
- [SAP Cloud Connector documentation](https://help.sap.com/docs/connectivity)
- [SAP S/4HANA Sourcing and Procurement](https://help.sap.com/)

> **Important:** SAP transactions, integration flows, configuration, supported features, APIs, document mappings, and Cloud Connector settings can vary by SAP release and customer architecture. Use this guide for interview preparation and conceptual troubleshooting; verify implementation-specific details against the applicable SAP documentation.

---

# Quick Revision

```text
SAP ARIBA
   ↓
P2O / S2C
   ↓
BUSINESS NETWORK
   ↓
MANAGED GATEWAY / CIG
   ↓
CLOUD CONNECTOR
   ↓
SAP ECC / S/4HANA
   ↓
SAP MM / FI
   ↓
BUSINESS PROCESSING
```

```text
WHEN SOMETHING FAILS:

What document?
      ↓
What direction?
      ↓
Last successful layer?
      ↓
What payload?
      ↓
What mapping?
      ↓
What master data?
      ↓
What exact error?
      ↓
What root cause?
      ↓
Is retry safe?
      ↓
Validate result
```

> **Core principle:** Do not troubleshoot by guessing the product that is "broken." Trace the transaction until the first failed layer is supported by evidence.
