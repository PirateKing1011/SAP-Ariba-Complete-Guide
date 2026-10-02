# SAP Ariba Architecture — Ariba → Managed Gateway/CIG → Cloud Connector → ECC / S/4HANA

A practical architecture reference for understanding how SAP Ariba solutions exchange procurement and supplier-related transactions with SAP ERP or SAP S/4HANA.

> **Terminology:** "CIG" is the common historical/project term. SAP's current product name is **SAP Integration Suite, managed gateway for spend management and SAP Business Network**. This guide uses Managed Gateway / CIG where useful.
>
> Exact components, interfaces, authentication, and document flows depend on the solution, ERP/S/4HANA release, integration scenario, and customer landscape.

---

## 1. Big Picture

```text
                    SAP ARIBA
               / SAP BUSINESS NETWORK
                         │
                         │ cXML / API / HTTPS
                         ▼
        ┌─────────────────────────────────┐
        │ SAP Integration Suite,          │
        │ Managed Gateway for Spend       │
        │ Management and SAP Business     │
        │ Network                          │
        │                                 │
        │ Historical/common term: CIG     │
        └───────────────┬─────────────────┘
                        │
                        ▼
        ┌─────────────────────────────────┐
        │ Integration / Middleware        │
        │ Mapping / Transformation        │
        │ Routing / Processing            │
        └───────────────┬─────────────────┘
                        │
                        ▼
        ┌─────────────────────────────────┐
        │ SAP Cloud Connector             │
        │ Secure cloud ↔ on-premise       │
        │ connectivity                    │
        └───────────────┬─────────────────┘
                        │
                        ▼
        ┌─────────────────────────────────┐
        │ SAP ECC / SAP S/4HANA          │
        │ API / IDoc / Proxy / Web       │
        │ Services / ERP Add-on          │
        └───────────────┬─────────────────┘
                        │
                        ▼
                  ERP Processing
```

SAP documents Managed Gateway integration with SAP ERP/S/4HANA and identifies Cloud Connector as a secure connectivity component between cloud services and on-premise systems.

---

## 2. Five Main Layers

| Layer | Role | Simple explanation |
|---|---|---|
| **SAP Ariba** | Business process | Buying, sourcing and procurement activities |
| **SAP Business Network** | Collaboration | Buyer ↔ supplier document exchange |
| **Managed Gateway / CIG** | Integration | Connects supported Ariba/Network scenarios with enterprise systems |
| **Cloud Connector** | Connectivity | Secure connection to selected on-premise resources |
| **ECC / S/4HANA** | ERP processing | Backend purchasing, receiving, invoicing and business processing |

### Mental model

```text
Ariba
= Business application

Business Network
= Buyer ↔ Supplier collaboration

Managed Gateway / CIG
= Integration layer

Cloud Connector
= Secure connectivity

ECC / S/4HANA
= ERP backend
```

---

# 3. SAP Ariba Layer

SAP Ariba provides cloud business applications such as:

- SAP Ariba Buying
- SAP Ariba Buying and Invoicing
- SAP Ariba Sourcing
- SAP Ariba Contracts
- SAP Ariba Supplier Lifecycle and Performance
- SAP Ariba Catalog
- SAP Business Network

A simplified procurement flow is:

```text
User
 ↓
Shopping
 ↓
Purchase Requisition
 ↓
Approval
 ↓
Purchase Order
```

The transaction may then move to a supplier, Business Network, or ERP depending on the configured scenario.

---

# 4. SAP Business Network Layer

Business Network provides buyer-supplier collaboration.

```text
BUYER
  │
  │ Purchase Order
  ▼
SAP BUSINESS NETWORK
  │
  ▼
SUPPLIER
  │
  ├── Order Confirmation
  ├── ASN
  └── Invoice
  │
  ▼
SAP BUSINESS NETWORK
  │
  ▼
BUYER
```

Important concepts include:

- trading relationships
- supplier accounts
- routing
- document exchange
- supplier collaboration
- transaction status

Business Network should therefore be understood separately from the buyer-side procurement application.

---

# 5. Managed Gateway / CIG

Managed Gateway is the integration capability connecting supported SAP Ariba / Business Network scenarios with enterprise systems.

Conceptually:

```text
Receive
  ↓
Validate
  ↓
Identify transaction
  ↓
Map / Transform
  ↓
Route
  ↓
Send
```

Depending on the scenario, integration may involve:

- cXML
- XML
- APIs
- IDocs
- web services
- proxies
- mappings
- value mappings
- authentication
- monitoring
- error handling

Do **not** assume every transaction uses the same technical path.

SAP's current documentation uses the name **SAP Integration Suite, managed gateway for spend management and SAP Business Network**. 

---

# 6. Cloud Connector

SAP Cloud Connector provides secure connectivity between SAP cloud services and on-premise systems.

```text
                 CLOUD
                   │
      Managed Gateway / Integration
                   │
                   ▼
        ┌──────────────────┐
        │ Cloud Connector  │
        └────────┬─────────┘
                 │
          Secure access to
          permitted resources
                 │
                 ▼
              ECC / S4
```

SAP describes Cloud Connector as an on-premise component that acts as a secure link/reverse-invoke proxy between cloud services and existing on-premise systems. 

### Cloud Connector is NOT

- the ERP
- the procurement application
- the main business-rule engine
- automatically the cause of every integration failure

Remember:

> **Cloud Connector = secure cloud ↔ on-premise connectivity.**

---

# 7. ECC / S/4HANA Layer

The ERP backend performs business processing.

It can contain:

- supplier/vendor data
- material data
- plant
- company code
- purchasing organization
- purchasing group
- accounting data
- purchase orders
- goods receipts
- invoices
- financial documents

```text
SAP ECC
   OR
SAP S/4HANA
```

The integration method depends on the customer's architecture and supported scenario.

---

# 8. ECC vs S/4HANA

| Area | ECC | S/4HANA |
|---|---|---|
| ERP backend | Yes | Yes |
| Ariba integration | Supported scenarios | Supported scenarios |
| Managed Gateway | Supported scenarios | Supported scenarios |
| Cloud Connector | Can be used | Can be used |
| IDoc | Common | Supported depending on scenario |
| APIs | Available | Important integration option |
| Proxy/Web Services | Can be used | Can be used |
| Add-on-based integration | Supported scenarios | Supported scenarios |
| API-based integration | Scenario dependent | Important option |

SAP documents both **add-on-based** and **API-based** integration methods for SAP ERP/S/4HANA scenarios.

---

# 9. Add-On-Based Architecture

A common architecture is:

```text
SAP Ariba / Business Network
            ↓
Managed Gateway / CIG
            ↓
Integration / Mapping
            ↓
Cloud Connector
            ↓
SAP ECC / S/4HANA
            ↓
Managed Gateway Add-On
            ↓
ERP Business Processing
```

SAP documents Managed Gateway add-ons for SAP ERP and SAP S/4HANA in add-on-based scenarios.

---

# 10. API-Based Architecture

Some S/4HANA scenarios can use APIs:

```text
SAP Ariba
    ↓
Managed Gateway / Integration
    ↓
API
    ↓
SAP S/4HANA
    ↓
Business Object / Application
```

SAP identifies API-based integration using SAP S/4HANA APIs as one supported integration approach, with hybrid scenarios possible in certain architectures. 
Therefore:

> **Do not assume every Ariba → S/4HANA transaction must be an IDoc.**

Always identify the actual integration scenario.

---

# 11. Ariba → ERP Flow

For a transaction moving from Ariba toward ERP:

```text
SAP ARIBA
    │
    ▼
BUSINESS NETWORK / ARIBA SERVICES
    │
    ▼
MANAGED GATEWAY / CIG
    │
    ▼
INTEGRATION / MAPPING
    │
    ▼
CLOUD CONNECTOR
    │
    ▼
ECC / S/4HANA
    │
    ▼
ERP INTERFACE
    │
    ▼
BUSINESS PROCESSING
```

The exact document and direction depend on the integration scenario.

---

# 12. ERP → Ariba Flow

The reverse direction:

```text
ECC / S/4HANA
      │
      ▼
ERP Interface
      │
      ▼
Integration / Middleware
      │
      ▼
Managed Gateway / CIG
      │
      ▼
SAP Ariba / Business Network
```

SAP's installation documentation describes outbound ERP transactions flowing through integration components to SAP Ariba, while inbound Ariba transactions can pass through Managed Gateway, integration components and Cloud Connector to ERP/S/4HANA.

---

# 13. Complete Architecture

```text
                         ┌──────────────────────┐
                         │      SAP ARIBA       │
                         │  Buying / Sourcing   │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │ SAP BUSINESS NETWORK │
                         │ Buyer ↔ Supplier     │
                         └──────────┬───────────┘
                                    │
                                    │ cXML / APIs /
                                    │ supported messages
                                    ▼
                    ┌──────────────────────────────┐
                    │     MANAGED GATEWAY / CIG    │
                    │ Integration / Routing / Map  │
                    └──────────────┬───────────────┘
                                   │
                                   ▼
                    ┌──────────────────────────────┐
                    │ Integration / Middleware     │
                    │ Transform / Map / Route      │
                    └──────────────┬───────────────┘
                                   │
                                   ▼
                    ┌──────────────────────────────┐
                    │       CLOUD CONNECTOR        │
                    │   Secure Cloud ↔ On-Prem     │
                    └──────────────┬───────────────┘
                                   │
                                   ▼
                    ┌──────────────────────────────┐
                    │        SAP ECC / S/4HANA     │
                    │ API / IDoc / Proxy / WS etc. │
                    └──────────────┬───────────────┘
                                   │
                                   ▼
                    ┌──────────────────────────────┐
                    │      ERP BUSINESS LOGIC      │
                    └──────────────────────────────┘
```

---

# 14. Master Data Flow

Master data can also move between systems:

```text
ECC / S4
   │
   │ Supplier / Material / Plant /
   │ Purchasing / Accounting data
   ▼
Integration
   ▼
Managed Gateway
   ▼
SAP Ariba
```

The exact master-data objects and direction depend on the configured integration scenario.

Typical failure pattern:

```text
Wrong Master Data
       ↓
Transaction Created
       ↓
Integration
       ↓
ERP Validation
       ↓
Rejected
```

---

# 15. PO Example

### Business flow

```text
Buyer
 ↓
SAP Ariba
 ↓
Purchase Order
 ↓
SAP Business Network
 ↓
Supplier
```

### ERP integration example

```text
ECC / S4
 ↓
Integration
 ↓
Managed Gateway
 ↓
SAP Ariba / Business Network
 ↓
Supplier
```

For a document coming from Ariba/Network into ERP:

```text
Supplier / Ariba
       ↓
Business Network
       ↓
Managed Gateway
       ↓
Integration
       ↓
Cloud Connector
       ↓
ECC / S4
```

The exact direction must always be defined relative to the system being discussed.

---

# 16. Troubleshooting by Architecture Layer

Do not immediately say:

> "CIG issue."

Trace the layers.

| Layer | Typical problem |
|---|---|
| SAP Ariba | Configuration / transaction issue |
| Business Network | Trading relationship / routing |
| Managed Gateway | Integration processing |
| Mapping | Field/value transformation |
| Authentication | Credentials/certificate |
| Middleware | Processing/routing failure |
| Cloud Connector | Connectivity/resource access |
| ERP interface | IDoc/API/web-service issue |
| ECC/S/4 application | Business validation |
| Master data | Missing/invalid business data |

### Troubleshooting flow

```text
Transaction failed
      ↓
Where did it stop?
      ↓
Ariba?
      ↓
Business Network?
      ↓
Managed Gateway?
      ↓
Middleware?
      ↓
Cloud Connector?
      ↓
ECC / S4 interface?
      ↓
ERP application?
      ↓
Master data / configuration?
```

---

# 17. Do Not Mix These Components

| Component | Remember it as |
|---|---|
| **SAP Ariba** | Business application |
| **Business Network** | Buyer ↔ supplier collaboration |
| **Managed Gateway / CIG** | Integration |
| **Cloud Connector** | Secure connectivity |
| **ECC** | ERP |
| **S/4HANA** | ERP |
| **cXML** | Business document/message format used in supported scenarios |
| **IDoc** | SAP integration document technology |
| **API** | Application interface |
| **Mapping** | Data transformation/conversion |

---

# 18. Interview Questions

### Q1. What is CIG?

CIG is the common historical/project term for the SAP integration capability now documented as **SAP Integration Suite, managed gateway for spend management and SAP Business Network**.

### Q2. What is Cloud Connector?

A secure connectivity component connecting cloud services with selected on-premise resources.

### Q3. Is Cloud Connector the same as CIG?

No.

```text
Managed Gateway
= Integration

Cloud Connector
= Secure connectivity
```

### Q4. Does every Ariba integration use IDocs?

No. The actual interface depends on the integration scenario and may use APIs, IDocs, proxies, web services, or other supported mechanisms.

### Q5. Where does the ERP add-on sit?

On the SAP ERP/S/4HANA side in add-on-based integration scenarios.

### Q6. If ECC rejects the transaction, is it automatically a CIG issue?

No. Identify the failure layer first. An ECC business validation, master-data problem, or ERP interface issue is not automatically a Managed Gateway failure.

---

# 19. Quick Revision

```text
SAP ARIBA
    ↓
Business Process
    ↓
BUSINESS NETWORK
    ↓
Managed Gateway / CIG
    ↓
Integration / Mapping
    ↓
CLOUD CONNECTOR
    ↓
ECC / S/4HANA
    ↓
ERP BUSINESS PROCESSING
```

Remember:

> **Ariba = Business process**

> **Business Network = Buyer ↔ Supplier collaboration**

> **Managed Gateway / CIG = Integration**

> **Cloud Connector = Secure connectivity**

> **ECC / S/4HANA = ERP processing**

---

# 20. Official References

- [SAP Integration Suite, Managed Gateway for Spend Management and SAP Business Network](https://help.sap.com/docs/sisgw)
- [Managed Gateway Installation Guide](https://help.sap.com/docs/sisgw/sap-ariba-cloud-integration-gateway-installation-guide)
- [Managed Gateway Configuration Guide](https://help.sap.com/docs/sisgw/sap-integration-suite-managed-gateway-for-spend-management-and-sap-business-network-configuration-guide)
- [SAP Cloud Connector](https://help.sap.com/docs/connectivity/sap-btp-connectivity-cf/cloud-connector)
- [SAP Integration Suite](https://help.sap.com/docs/integration-suite)

SAP documentation should be checked for release-specific architecture, prerequisites, supported scenarios, and configuration because these can vary by release and customer landscape.

---

## Core Idea

```text
Business process starts in Ariba
             ↓
Business Network / Integration
             ↓
Managed Gateway
             ↓
Cloud Connector
             ↓
ECC / S/4HANA
             ↓
ERP business processing
```

**Think in layers, not just products.**

When troubleshooting, always ask:

> **Where did the transaction stop?**
