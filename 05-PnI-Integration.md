# SAP Ariba PnI --- Platform & Integration Complete Guide

> **PnI = Platform and Integration**
>
> A practical technical guide covering SAP Ariba integration
> architecture, CIG / SAP Integration Suite Managed Gateway, SAP Cloud
> Connector, SAP Integration Suite / Cloud Integration, SAP ECC,
> cXML/XML, payloads, inbound/outbound flows, authentication, APIs,
> mappings, monitoring, analysis, and troubleshooting.

## Table of Contents

1.  [PnI Fundamentals](#1-pni-fundamentals)
2.  [CIG and Managed Gateway](#2-cig-and-managed-gateway)
3.  [End-to-End Architecture](#3-end-to-end-architecture)
4.  [SAP ECC](#4-sap-ecc)
5.  [SAP Ariba Platform](#5-sap-ariba-platform)
6.  [Cloud Connector](#6-cloud-connector)
7.  [SAP Integration Suite / Cloud
    Integration](#7-sap-integration-suite--cloud-integration)
8.  [XML and cXML](#8-xml-and-cxml)
9.  [Payload Analysis](#9-payload-analysis)
10. [Inbound and Outbound](#10-inbound-and-outbound)
11. [Integration Flows](#11-integration-flows)
12. [Document Types](#12-document-types)
13. [Authentication and Security](#13-authentication-and-security)
14. [APIs and Interfaces](#14-apis-and-interfaces)
15. [Mappings and Cross-References](#15-mappings-and-cross-references)
16. [Synchronous vs Asynchronous](#16-synchronous-vs-asynchronous)
17. [Monitoring and Transaction
    Analysis](#17-monitoring-and-transaction-analysis)
18. [Error Classification](#18-error-classification)
19. [Troubleshooting Methodology](#19-troubleshooting-methodology)
20. [Common Issues](#20-common-issues)
21. [End-to-End Troubleshooting
    Scenarios](#21-end-to-end-troubleshooting-scenarios)
22. [Testing Strategy](#22-testing-strategy)
23. [Support Runbook](#23-support-runbook)
24. [Implementation Checklist](#24-implementation-checklist)
25. [Interview Questions](#25-interview-questions)
26. [Quick Revision](#26-quick-revision)
27. [Official References](#27-official-references)

------------------------------------------------------------------------

# 1. PnI Fundamentals

PnI is the technical layer connecting SAP Ariba solutions, SAP Business
Network and enterprise backends such as SAP ECC/S/4HANA.

The key question is not only:

> "Did the transaction leave Ariba?"

The real question is:

> "At which layer did the transaction stop, and why?"

A typical path is:

``` text
SAP Ariba / Business Network
          |
          v
CIG / Managed Gateway
          |
          v
SAP Integration Suite / Middleware
          |
          v
SAP Cloud Connector
          |
          v
SAP ECC / S4
          |
          v
SAP business processing
```

PnI covers:

-   Connectivity
-   Authentication
-   Authorization
-   XML/cXML
-   APIs
-   IDocs
-   Proxies
-   SOAP/HTTP
-   Mapping
-   Value mapping
-   Cross-references
-   Routing
-   Monitoring
-   Error handling
-   Reprocessing

## PnI vs P2O

P2O explains **what the procurement process does**.

PnI explains **how the systems exchange the information required by that
process**.

Example:

``` text
P2O:
Requisition -> Approval -> PO -> Receipt -> Invoice

PnI:
PO message -> mapping -> cXML -> gateway -> network
Invoice message -> gateway -> middleware -> ECC
```

------------------------------------------------------------------------

# 2. CIG and Managed Gateway

## 2.1 What is CIG?

CIG means **SAP Ariba Cloud Integration Gateway**.

SAP's current terminology uses **SAP Integration Suite, managed gateway
for spend management and SAP Business Network**.

You will encounter both names in real projects.

``` text
CIG
= common/legacy project terminology

Managed Gateway
= current SAP terminology
```

Do not assume that "CIG" automatically means an obsolete implementation.

## 2.2 What does CIG/Managed Gateway do?

Conceptually:

``` text
Receive
  |
Validate
  |
Transform
  |
Map
  |
Route
  |
Deliver
  |
Track
```

It can provide capabilities around:

-   Transaction processing
-   Validation
-   Transformation
-   Mapping
-   Cross-references
-   Connectivity
-   Monitoring
-   Payload inspection
-   Reprocessing

## 2.3 Important tools

Depending on the current product/release and scenario, the managed
gateway environment provides tools such as:

-   Transaction Tracker
-   Document Validator
-   Connectivity testing
-   Transformation/mapping capabilities
-   Integration project configuration

A current SAP Help page states that Transaction Tracker can search
transactions and download source payloads, target payloads and
attachments; it also supports transaction reprocessing.

------------------------------------------------------------------------

# 3. End-to-End Architecture

## 3.1 Typical Ariba + ECC architecture

``` text
                    SAP ARIBA
                        |
                        | HTTPS / cXML / API
                        v
             +-------------------------+
             | CIG / Managed Gateway   |
             |                         |
             | Validation              |
             | Mapping                 |
             | Transformation          |
             | Routing                 |
             | Monitoring              |
             +------------+------------+
                          |
                          v
             +-------------------------+
             | SAP Integration Suite   |
             | / Cloud Integration     |
             +------------+------------+
                          |
                          v
             +-------------------------+
             | SAP Cloud Connector     |
             +------------+------------+
                          |
                    Secure Tunnel
                          |
                          v
             +-------------------------+
             | SAP ECC / S4            |
             |                         |
             | IDoc / Proxy / API      |
             | Business Processing     |
             +-------------------------+
```

The exact architecture depends on:

-   SAP product
-   release
-   integration scenario
-   customer architecture
-   direct vs mediated connectivity
-   middleware
-   authentication method

Therefore this diagram is a conceptual reference, not a universal
implementation.

## 3.2 Architecture questions

For every integration, identify:

``` text
Who sends?
Who receives?
Which interface?
Which protocol?
Which endpoint?
Which authentication?
Which mapping?
Which middleware?
Where is it monitored?
```

------------------------------------------------------------------------

# 4. SAP ECC

ECC is often the enterprise backend in SAP Ariba projects.

It can contain:

-   Company codes
-   Plants
-   Purchasing organizations
-   Purchasing groups
-   Suppliers
-   Materials
-   Material groups
-   UOM
-   Currency
-   Cost centers
-   GL accounts
-   Purchase orders
-   Goods receipts
-   Invoices

## 4.1 ECC is not just storage

A common misconception:

``` text
Ariba -> XML -> ECC
```

The actual process is closer to:

``` text
Ariba
  |
Gateway
  |
Middleware
  |
ECC interface
  |
ECC validation
  |
Application processing
  |
Business document
```

A technically valid XML message can still fail in ECC.

Example:

``` text
XML valid
Mapping successful
Connectivity successful
        |
        v
ECC receives message
        |
        v
Plant does not exist
        |
        v
Business failure
```

## 4.2 ECC monitoring tools

Common tools include:

  Tool          Typical purpose
  ------------- -----------------------------------------
  SLG1          Application logs
  WE02 / WE05   IDoc monitoring
  BD87          IDoc reprocessing
  SRT_MONI      Web-service monitoring where applicable
  SM58          tRFC monitoring where applicable
  SM37          Background jobs
  ST22          ABAP dumps
  SM21          System log
  SU53          Authorization analysis
  SPRO          Configuration

Exact tools depend on the interface and ECC release.

------------------------------------------------------------------------

# 5. SAP Ariba Platform

From an integration perspective, identify the actual source/target
application.

Possible participants include:

-   SAP Ariba Procurement
-   SAP Ariba Buying
-   SAP Ariba Buying and Invoicing
-   SAP Ariba Strategic Sourcing
-   SAP Ariba Supplier Lifecycle and Performance
-   SAP Business Network
-   Supplier systems
-   SAP ECC
-   SAP S/4HANA

Do not say only:

> "Ariba sent it."

Instead identify:

``` text
Application
+
document
+
sender
+
receiver
+
direction
```

------------------------------------------------------------------------

# 6. Cloud Connector

## 6.1 What is Cloud Connector?

SAP Cloud Connector provides controlled connectivity between cloud
services on SAP BTP and on-premise systems.

Conceptually:

``` text
Cloud
 |
 v
Cloud Integration
 |
 v
Cloud Connector
 |
 | secure tunnel
 v
ECC
```

SAP describes Cloud Connector as an on-premise agent and reverse invoke
proxy that allows controlled access to internal systems without exposing
the entire internal landscape.

## 6.2 Why use it?

Instead of:

``` text
Internet
   |
   v
Entire ECC
```

use:

``` text
Cloud
 |
 v
Cloud Connector
 |
 +-- Allowed host
 +-- Allowed port
 +-- Allowed resources
 |
 v
ECC
```

## 6.3 Important concepts

Know:

-   BTP subaccount
-   Cloud Connector instance
-   On-premise system
-   Virtual host
-   Internal host
-   Port
-   Access control
-   Resources
-   Tunnel
-   Connectivity status

## 6.4 Cloud Connector troubleshooting

Check in order:

1.  Is Cloud Connector running?
2.  Is the BTP subaccount connected?
3.  Is the tunnel established?
4.  Is the correct on-premise system configured?
5.  Is virtual host correct?
6.  Is internal host correct?
7.  Is port correct?
8.  Is required resource/path exposed?
9.  Can the Cloud Connector host reach ECC?
10. Is a firewall/proxy blocking traffic?

------------------------------------------------------------------------

# 7. SAP Integration Suite / Cloud Integration

Cloud Integration can be used to build integration flows between
systems.

Conceptually:

``` text
Sender
  |
  v
Sender Adapter
  |
  v
Integration Flow
  |
  +-- Validation
  +-- Mapping
  +-- Value Mapping
  +-- Transformation
  +-- Routing
  |
  v
Receiver Adapter
  |
  v
Receiver
```

Potential technologies include:

-   HTTP
-   SOAP
-   REST
-   IDoc
-   OData
-   RFC
-   APIs
-   XML
-   JSON

## 7.1 Do not confuse CIG and Cloud Integration

They may participate in the same architecture, but they are not simply
two names for one component.

A customer may have:

``` text
Ariba
  |
Managed Gateway
  |
Cloud Integration
  |
Cloud Connector
  |
ECC
```

The exact topology depends on the integration scenario.

------------------------------------------------------------------------

# 8. XML and cXML

## 8.1 XML

XML is a general markup language.

``` xml
<Order>
    <OrderNumber>4500001234</OrderNumber>
    <Supplier>ABC</Supplier>
    <Amount>12500</Amount>
</Order>
```

## 8.2 cXML

cXML means **commerce eXtensible Markup Language**.

It is an XML-based standard widely used for commerce/procurement
transactions.

Typical document examples include:

-   OrderRequest
-   ConfirmationRequest
-   ShipNoticeRequest
-   ReceiptRequest
-   InvoiceDetailRequest
-   StatusUpdateRequest
-   QuoteRequest
-   ServiceEntryRequest

The exact supported documents depend on the solution and integration
scenario.

## 8.3 XML vs cXML

``` text
XML
 |
 +-- General markup language

cXML
 |
 +-- XML-based commerce/procurement standard
```

Good interview answer:

> XML is the general markup technology, while cXML is an XML-based
> standard designed for electronic commerce and procurement document
> exchange.

------------------------------------------------------------------------

# 9. Payload Analysis

A payload is the actual message exchanged between systems.

Example educational cXML:

``` xml
<?xml version="1.0" encoding="UTF-8"?>

<cXML payloadID="123456789"
      timestamp="2026-10-01T08:30:00Z">

    <Header>

        <From>
            <Credential domain="NetworkID">
                <Identity>BUYER123</Identity>
            </Credential>
        </From>

        <To>
            <Credential domain="NetworkID">
                <Identity>SUPPLIER456</Identity>
            </Credential>
        </To>

        <Sender>
            <Credential domain="NetworkID">
                <Identity>BUYER_SYSTEM</Identity>
            </Credential>
            <UserAgent>Example Integration</UserAgent>
        </Sender>

    </Header>

    <Request deploymentMode="production">

        <OrderRequest>

            <OrderRequestHeader
                orderID="4500001234"
                orderDate="2026-10-01T08:30:00Z">

                <Total>
                    <Money currency="INR">125000</Money>
                </Total>

            </OrderRequestHeader>

        </OrderRequest>

    </Request>

</cXML>
```

This is a learning example, not a production payload.

## 9.1 What to inspect

### Header

-   payload ID
-   timestamp
-   sender
-   receiver
-   credential domain
-   identity

### Request

-   document type
-   deployment mode
-   transaction number
-   document date

### Business data

-   supplier
-   company code
-   plant
-   material
-   quantity
-   UOM
-   currency
-   price
-   account assignment
-   delivery information

### References

-   PO number
-   requisition number
-   invoice number
-   supplier ID
-   ERP reference

## 9.2 Payload analysis sequence

``` text
1. Identify document
2. Identify transaction ID
3. Identify sender
4. Identify receiver
5. Check mandatory fields
6. Check formats
7. Check mapping
8. Check master data
9. Check business validity
```

------------------------------------------------------------------------

# 10. Inbound and Outbound

Inbound/outbound is always **relative to a system**.

## 10.1 ECC perspective

``` text
Ariba -> ECC
       = INBOUND

ECC -> Ariba
       = OUTBOUND
```

## 10.2 Ariba perspective

``` text
ECC -> Ariba
       = INBOUND

Ariba -> ECC
       = OUTBOUND
```

Therefore the correct support question is:

> "Inbound or outbound from which system?"

## 10.3 Typical examples

  Transaction                      ECC perspective
  -------------------------------- -----------------
  PO sent from ECC to Network      Outbound
  PO change sent from ECC          Outbound
  Receipt sent from ECC            Outbound
  Invoice received from Network    Inbound
  PR request received from Ariba   Inbound
  PO request received from Ariba   Inbound
  Master data sent ECC -\> Ariba   Outbound

Exact direction depends on the configured scenario.

------------------------------------------------------------------------

# 11. Integration Flows

## 11.1 ECC -\> Ariba / Network

Example purchase order:

``` text
ECC
 |
 | Purchase Order
 v
ECC Interface
 |
 | IDoc / Proxy / other interface
 v
Cloud Integration
 |
 v
Managed Gateway
 |
 | Validation / Mapping
 v
cXML
 |
 v
Business Network / Ariba
 |
 v
Supplier
```

Possible failure points:

-   PO output not triggered
-   IDoc/proxy failure
-   middleware failure
-   authentication
-   mapping
-   XML validation
-   network routing
-   supplier enablement

## 11.2 Ariba -\> ECC

Example PO request:

``` text
Ariba
 |
 | PurchaseOrderRequest
 v
Managed Gateway
 |
 | Validation / Transformation
 v
Cloud Integration
 |
 v
Cloud Connector
 |
 v
ECC
 |
 | Proxy / IDoc / API
 v
ECC business processing
```

Possible failures:

-   supplier invalid
-   plant invalid
-   company code invalid
-   purchasing organization invalid
-   missing account assignment
-   mapping issue
-   authentication
-   connectivity
-   backend validation

## 11.3 Invoice flow

Conceptual example:

``` text
Supplier
 |
 v
Business Network
 |
 v
Managed Gateway
 |
 v
Integration Layer
 |
 v
Cloud Connector
 |
 v
ECC
 |
 v
Invoice processing
```

If invoice is missing in ECC, trace each layer rather than assuming the
gateway is the problem.

------------------------------------------------------------------------

# 12. Document Types

Common cXML document examples:

  Business purpose     cXML document
  -------------------- ----------------------
  Purchase order       OrderRequest
  Order confirmation   ConfirmationRequest
  Ship notice / ASN    ShipNoticeRequest
  Goods receipt        ReceiptRequest
  Invoice              InvoiceDetailRequest
  Status update        StatusUpdateRequest
  Quote                QuoteRequest
  Service entry        ServiceEntryRequest

These are examples, not a guarantee that every customer/solution
supports every document in exactly the same way.

------------------------------------------------------------------------

# 13. Authentication and Security

Authentication asks:

> Who are you?

Authorization asks:

> What are you allowed to do?

These are different.

## 13.1 Common mechanisms

Depending on the scenario:

-   Basic authentication
-   User ID/password
-   X.509 certificate
-   Mutual TLS
-   OAuth/client credentials
-   BTP service instances/service keys
-   Technical SAP users
-   RFC destinations
-   HTTPS/TLS

## 13.2 Basic authentication

``` text
Client
 |
 | username/password
 v
Server
 |
 +-- Authenticate
 |
 +-- Authorize
```

Possible failures:

-   wrong username
-   wrong password
-   expired password
-   locked user
-   wrong endpoint
-   wrong environment
-   wrong authentication method

## 13.3 Certificate authentication

``` text
Client
 |
 | Client certificate
 v
Server
 |
 +-- Certificate validation
 +-- Trust validation
 +-- Identity mapping
```

Possible problems:

-   expired certificate
-   incorrect certificate
-   certificate not trusted
-   missing certificate chain
-   wrong private key
-   incorrect mapping
-   certificate installed in wrong environment

## 13.4 Environment mismatch

Classic mistake:

``` text
TEST credential + PROD endpoint
```

or:

``` text
PROD credential + TEST endpoint
```

Always verify:

``` text
Environment
+
Endpoint
+
Credential
+
Certificate
```

------------------------------------------------------------------------

# 14. APIs and Interfaces

An API is a defined interface for programmatic communication.

Common integration technologies:

-   REST
-   HTTP
-   SOAP
-   OData
-   RFC
-   IDoc
-   cXML endpoints

## 14.1 REST

``` text
POST /orders
GET  /orders/12345
```

JSON is common, but XML can also be transported.

## 14.2 SOAP

SOAP commonly uses XML:

``` text
Client
 |
 | SOAP request
 v
Service
 |
 | SOAP response
 v
Client
```

## 14.3 IDoc

IDoc is a common SAP message exchange mechanism.

``` text
ECC
 |
 v
IDoc
 |
 v
Middleware
 |
 v
Target
```

When troubleshooting:

-   IDoc number
-   status
-   message type
-   basic type
-   partner
-   segment values
-   error message
-   application document

## 14.4 Proxy

A proxy is an SAP-generated service interface.

``` text
ECC ABAP
 |
 v
Proxy
 |
 v
XML/SOAP
 |
 v
Middleware
```

## 14.5 API vs cXML

They are different concepts:

``` text
API
= communication/interface mechanism

cXML
= document/message format
```

An API endpoint may transport cXML.

------------------------------------------------------------------------

# 15. Mappings and Cross-References

## 15.1 Mapping

Mapping converts source representation to target representation.

``` text
Source:
Company Code = 1000

       |
       v

Target:
CompanyCode = IN01
```

## 15.2 Value mapping

Example:

``` text
Ariba Plant = BLR01
ECC Plant   = 1001
```

Mapping:

``` text
BLR01 <-> 1001
```

## 15.3 Why mappings fail

-   source value missing
-   target value missing
-   mapping missing
-   mapping inactive
-   wrong direction
-   wrong environment
-   old code
-   case sensitivity
-   leading zero
-   incorrect system identifier

## 15.4 Mapping troubleshooting

Ask:

``` text
What value came in?
What value should go out?
Is mapping required?
Does mapping exist?
Is it active?
Is the correct environment used?
Is direction correct?
```

------------------------------------------------------------------------

# 16. Synchronous vs Asynchronous

## Synchronous

Sender waits for response.

``` text
Sender
 |
 | Request
 v
Receiver
 |
 | Response
 v
Sender
```

Useful when immediate response is required.

## Asynchronous

Sender does not need to wait for final processing.

``` text
Sender
 |
 v
Queue / Integration
 |
 v
Receiver
```

Benefits:

-   decoupling
-   retries
-   resilience
-   volume processing

Troubleshooting is more distributed because the sender can finish while
downstream processing is still occurring.

------------------------------------------------------------------------

# 17. Monitoring and Transaction Analysis

## 17.1 Monitoring chain

``` text
Ariba / Network
       |
       v
Gateway
       |
       v
Middleware
       |
       v
Cloud Connector
       |
       v
ECC
```

Monitor each layer separately.

## 17.2 Gateway monitoring

Transaction Tracker can be used to search transaction documents using
criteria such as:

-   date/time
-   transaction number
-   status
-   document type
-   sender
-   receiver

It can expose transaction details and, where available, source/target
payloads and attachments.

Current SAP documentation describes statuses such as:

-   COMPLETED
-   ERROR
-   FAILED
-   PROCESSING
-   RETRY
-   DUMPED

Do not interpret a gateway `COMPLETED` status as proof that the final
ECC business document exists. Confirm downstream processing.

## 17.3 Middleware monitoring

Check:

-   integration flow status
-   message ID
-   exception
-   mapping failure
-   adapter failure
-   HTTP response
-   SOAP fault
-   retry
-   routing

## 17.4 ECC monitoring

Depending on the interface:

``` text
SLG1
WE02 / WE05
BD87
SRT_MONI
ST22
SM21
SM37
SU53
```

Use the appropriate monitor for the interface technology.

------------------------------------------------------------------------

# 18. Error Classification

Never label every failed transaction a "CIG issue."

## Layer 1 --- Network

Examples:

-   DNS
-   firewall
-   timeout
-   proxy
-   unreachable host
-   TLS connectivity

## Layer 2 --- Authentication

Examples:

-   401
-   expired password
-   invalid certificate
-   certificate trust failure

## Layer 3 --- Authorization

Examples:

-   403
-   missing role
-   resource access denied

## Layer 4 --- XML / Schema

Examples:

-   malformed XML
-   missing mandatory element
-   invalid namespace
-   invalid data type

## Layer 5 --- Mapping

Examples:

-   mapping missing
-   target value unavailable
-   transformation failure

## Layer 6 --- Gateway / Middleware

Examples:

-   adapter error
-   route failure
-   deployment failure
-   integration-flow exception

## Layer 7 --- ECC Technical

Examples:

-   IDoc error
-   proxy error
-   web-service error
-   ABAP dump
-   RFC issue

## Layer 8 --- ECC Business

Examples:

-   invalid plant
-   invalid supplier
-   invalid company code
-   missing GL account
-   invalid purchasing organization

## Layer 9 --- Ariba Business Configuration

Examples:

-   supplier setup
-   network relationship
-   configuration
-   business rule
-   document configuration

------------------------------------------------------------------------

# 19. Troubleshooting Methodology

Use this exact approach.

## Step 1 --- Collect identifiers

Request:

``` text
Environment
Document type
Transaction ID
Business document number
Date/time
Sender
Receiver
Exact error
```

## Step 2 --- Determine direction

``` text
Ariba -> ECC?
ECC -> Ariba?
Network -> ECC?
ECC -> Network?
```

## Step 3 --- Locate the transaction

Search the gateway.

``` text
FOUND
 |
 +-- read status
 +-- read error
 +-- download payload

NOT FOUND
 |
 +-- investigate source/interface/trigger
```

## Step 4 --- Read the exact error

Do not troubleshoot from:

> Transaction failed.

Get the actual message.

## Step 5 --- Inspect payload

Compare:

``` text
Source payload
      vs
Target payload
```

## Step 6 --- Identify failure layer

``` text
Network?
Authentication?
Authorization?
XML?
Mapping?
Gateway?
Middleware?
Cloud Connector?
ECC interface?
ECC business?
```

## Step 7 --- Fix root cause

Do not repeatedly retry an unchanged bad payload.

## Step 8 --- Reprocess carefully

Before reprocessing:

-   Confirm root cause fixed
-   Confirm target did not already create the document
-   Check duplicate risk
-   Check whether reprocessing is supported for the scenario
-   Confirm downstream systems are ready

## Step 9 --- Verify

Do not stop at:

> Message was reprocessed.

Confirm:

``` text
Transaction success
+
target received
+
business document exists
```

------------------------------------------------------------------------

# 20. Common Issues

## 20.1 Transaction not visible in gateway

### Symptoms

User says:

> Document was created but I cannot find it in CIG.

### Check

1.  Source document exists
2.  Interface/output was triggered
3.  Source job/interface is running
4.  Middleware received the message
5.  Correct gateway endpoint
6.  Correct environment

If the transaction never reached the gateway, do not start by changing
CIG mapping.

------------------------------------------------------------------------

## 20.2 401 Unauthorized

### Meaning

Authentication failed.

### Check

-   username
-   password
-   technical user
-   endpoint
-   environment
-   credential validity
-   authentication method

------------------------------------------------------------------------

## 20.3 403 Forbidden

### Meaning

Request was understood but access was denied.

### Check

-   authorization
-   Cloud Connector access control
-   user/technical-user roles
-   endpoint permissions
-   resource exposure

First identify which component returned the 403.

------------------------------------------------------------------------

## 20.4 404 Not Found

Potential causes:

-   wrong endpoint
-   wrong path
-   wrong virtual host mapping
-   incorrect API URL
-   resource not exposed

------------------------------------------------------------------------

## 20.5 408 / timeout

Potential causes:

-   network delay
-   firewall
-   proxy
-   backend response too slow
-   Cloud Connector path
-   service unavailable

Check the exact layer where timeout occurred.

------------------------------------------------------------------------

## 20.6 500 Internal Server Error

A 500 only tells you the server encountered an error.

Do not immediately conclude:

> ECC is broken.

Identify which component generated the 500 and inspect its logs.

------------------------------------------------------------------------

## 20.7 XML validation error

Check:

-   XML well-formedness
-   namespace
-   mandatory fields
-   element structure
-   data types
-   cXML/schema version
-   invalid characters

------------------------------------------------------------------------

## 20.8 Mapping error

Example:

``` text
Plant BLR01
     |
     v
Mapping lookup
     |
     X
No target value
```

Fix the mapping/value configuration, then test.

------------------------------------------------------------------------

## 20.9 ECC rejects valid XML

Example:

``` text
Gateway = successful
ECC = failed

Reason:
Plant 1001 invalid
```

This is primarily a backend business/configuration issue.

------------------------------------------------------------------------

## 20.10 Duplicate transaction

Possible causes:

-   manual resend
-   retry after uncertain response
-   source resend
-   timeout followed by resend
-   duplicate business key

Before reprocessing:

> Verify whether the target already created the document.

------------------------------------------------------------------------

# 21. End-to-End Troubleshooting Scenarios

## Scenario 1 --- Invoice missing in ECC

Flow:

``` text
Supplier
 |
 v
Business Network
 |
 v
Managed Gateway
 |
 v
Middleware
 |
 v
Cloud Connector
 |
 v
ECC
```

### Investigation

**1. Search Transaction Tracker**

If no transaction:

``` text
Investigate supplier/network/source
```

If failed:

``` text
Read exact error
```

If completed:

``` text
Continue downstream
```

**2. Check middleware**

-   message present?
-   flow completed?
-   exception?
-   receiver response?

**3. Check Cloud Connector**

-   tunnel?
-   resource?
-   host?
-   port?

**4. Check ECC**

-   interface?
-   IDoc/proxy?
-   application log?
-   business error?

### Key lesson

Trace the complete chain.

------------------------------------------------------------------------

## Scenario 2 --- PO reaches Network but supplier does not receive it

Flow:

``` text
ECC
 |
 v
Middleware
 |
 v
Gateway
 |
 v
Business Network
 |
 v
Supplier
```

If gateway is successful, investigate:

-   receiver identity
-   supplier/network relationship
-   document routing
-   supplier enablement
-   network status
-   supplier-side processing

Do not keep changing ECC configuration if the document already reached
the network.

------------------------------------------------------------------------

## Scenario 3 --- PO request fails in ECC

``` text
Ariba
 |
 v
Gateway
 |
 v
Middleware
 |
 v
Cloud Connector
 |
 v
ECC
```

Suppose the ECC error says:

``` text
Purchasing group missing
```

Classification:

``` text
Backend business/configuration
```

Not necessarily:

``` text
CIG problem
```

------------------------------------------------------------------------

## Scenario 4 --- Certificate failure

Symptoms:

``` text
TLS handshake failed
certificate expired
certificate not trusted
```

Check:

1.  Certificate expiry
2.  Certificate chain
3.  Correct certificate
4.  Trust configuration
5.  Environment
6.  Private key
7.  Client-certificate mapping

------------------------------------------------------------------------

## Scenario 5 --- Payload has missing CompanyCode

``` text
Source payload
      |
      v
CompanyCode missing
      |
      v
Mapping cannot populate it
      |
      v
Validation fails
```

Do not retry unchanged.

Determine whether:

-   source system omitted it
-   mapping is wrong
-   transformation removed it
-   business configuration is incomplete

------------------------------------------------------------------------

## Scenario 6 --- CIG says completed but ECC document does not exist

Do not assume success.

Trace:

``` text
Gateway
 |
 v
Middleware
 |
 v
Cloud Connector
 |
 v
ECC endpoint
 |
 v
ECC interface
 |
 v
ECC application
 |
 v
Business document
```

The failure can exist after the gateway stage.

------------------------------------------------------------------------

# 22. Testing Strategy

A good integration test plan includes more than the happy path.

## 22.1 Happy path

``` text
Create
 |
Send
 |
Receive
 |
Process
 |
Verify
```

## 22.2 Negative tests

Test:

-   invalid supplier
-   invalid plant
-   missing mandatory field
-   invalid currency
-   invalid UOM
-   invalid mapping
-   expired credentials
-   unreachable endpoint
-   malformed XML
-   duplicate transaction

## 22.3 Volume tests

Test:

``` text
1
10
100
large batch
```

Check:

-   processing time
-   queue behavior
-   retry
-   failures
-   duplicates

## 22.4 Reprocessing test

``` text
Failure
 |
Fix
 |
Reprocess
 |
Success
```

Also test that reprocessing a bad payload does not magically fix it.

------------------------------------------------------------------------

# 23. Support Runbook

## Ticket intake template

``` text
Environment:
TEST / PROD

Business Process:
P2O / S2C / Network

Document Type:

Business Document Number:

Transaction ID:

Sender:

Receiver:

Date/Time:

Exact Error:

Source System:

Target System:
```

## Investigation checklist

### Source

-   Was document created?
-   Was interface triggered?
-   Was output generated?

### Gateway

-   Transaction visible?
-   Status?
-   Document type?
-   Error?
-   Source payload?
-   Target payload?

### Middleware

-   Flow active?
-   Message present?
-   Exception?
-   HTTP status?
-   SOAP fault?
-   Mapping?

### Cloud Connector

-   Connected?
-   Tunnel?
-   Virtual host?
-   Internal host?
-   Port?
-   Resource exposed?

### ECC

-   IDoc/proxy?
-   Application log?
-   Authorization?
-   Dump?
-   Business validation?
-   Backend document?

### Resolution

-   Root cause
-   Fix
-   Reprocess?
-   Duplicate risk
-   Verification

------------------------------------------------------------------------

# 24. Implementation Checklist

## Architecture

-   [ ] Source and target systems identified
-   [ ] Test/production separated
-   [ ] Integration pattern documented
-   [ ] Endpoints documented securely

## Connectivity

-   [ ] Managed Gateway configured
-   [ ] Middleware configured where required
-   [ ] Cloud Connector configured
-   [ ] Virtual host configured
-   [ ] Internal host configured
-   [ ] Ports verified
-   [ ] Resources exposed

## Security

-   [ ] Technical users
-   [ ] Credentials
-   [ ] Certificates
-   [ ] Trust configuration
-   [ ] Authorization
-   [ ] Certificate expiry process

## Interfaces

-   [ ] Inbound
-   [ ] Outbound
-   [ ] Sender/receiver
-   [ ] Endpoints
-   [ ] Interface technologies
-   [ ] Error handling

## Mapping

-   [ ] Value mapping
-   [ ] Cross references
-   [ ] Supplier mapping
-   [ ] Plant mapping
-   [ ] Company code
-   [ ] UOM
-   [ ] Currency
-   [ ] Purchasing organization

## Monitoring

-   [ ] Transaction Tracker
-   [ ] Middleware monitor
-   [ ] Cloud Connector monitoring
-   [ ] ECC application logs
-   [ ] IDoc monitor
-   [ ] Web-service monitor where applicable

## Testing

-   [ ] Happy path
-   [ ] Negative test
-   [ ] Authentication failure
-   [ ] Mapping failure
-   [ ] Connectivity failure
-   [ ] Backend business failure
-   [ ] Reprocessing
-   [ ] Duplicate scenario
-   [ ] Volume test

------------------------------------------------------------------------

# 25. Interview Questions

## Q1. What is CIG?

CIG is the commonly used name for SAP Ariba Cloud Integration Gateway.
SAP's current terminology uses SAP Integration Suite, managed gateway
for spend management and SAP Business Network. It provides integration
capabilities between SAP Ariba/SAP Business Network and enterprise
systems.

## Q2. What is the role of CIG?

It can handle connectivity, validation, transformation,
mapping/cross-reference processing, routing, monitoring and supported
transaction processing.

## Q3. What is Cloud Connector?

Cloud Connector provides secure, controlled connectivity between cloud
services and on-premise systems. It acts as a reverse invoke proxy and
exposes selected resources rather than the entire internal system.

## Q4. What is cXML?

cXML is an XML-based standard used for electronic commerce and
procurement document exchange.

## Q5. XML vs cXML?

XML is a general markup technology. cXML is an XML-based
commerce/procurement standard.

## Q6. What is inbound/outbound?

Direction is relative to the system.

``` text
Ariba -> ECC = inbound to ECC
ECC -> Ariba = outbound from ECC
```

## Q7. What is a payload?

The actual message/data exchanged between systems.

## Q8. How do you troubleshoot a failed transaction?

I collect the transaction/document ID, environment, direction and exact
error. I locate it in gateway monitoring, inspect source and target
payloads, identify the failure layer, check middleware/Cloud
Connector/ECC logs, fix the root cause and reprocess only after
confirming duplicate safety.

## Q9. CIG says completed but ECC has no document. What do you do?

Trace downstream:

``` text
Gateway
-> Middleware
-> Cloud Connector
-> ECC interface
-> ECC application
```

A gateway completion does not automatically prove final
business-document creation.

## Q10. How do you troubleshoot 401?

Check:

-   endpoint
-   environment
-   username
-   password
-   technical user
-   authentication method
-   credential expiry

## Q11. How do you troubleshoot 403?

Identify the component returning the 403 and check authorization, Cloud
Connector access control, endpoint permissions and service-user roles.

## Q12. What is mapping?

Conversion of source representation into target representation.

## Q13. What is cross-reference?

A relationship between equivalent values in different systems.

``` text
Ariba BLR01 <-> ECC 1001
```

## Q14. What is an IDoc?

A structured SAP data exchange mechanism commonly used for integration.

## Q15. What is a proxy?

An SAP-generated service interface used for structured service-based
communication.

## Q16. What do you inspect in a payload?

-   sender
-   receiver
-   transaction ID
-   document number
-   mandatory fields
-   dates
-   quantity
-   UOM
-   currency
-   supplier
-   plant
-   references
-   mapping values

## Q17. What is a technical error vs business error?

Technical:

``` text
Timeout
Authentication
XML
Adapter
Network
```

Business:

``` text
Invalid supplier
Invalid plant
Invalid company code
Missing GL account
```

## Q18. How do you handle duplicate risk?

Before retry/reprocess, verify whether the target already created the
business document. Understand the transaction's identifiers and retry
behavior.

## Q19. What information do you ask for in an integration ticket?

``` text
Environment
Transaction ID
Business document number
Document type
Timestamp
Sender
Receiver
Exact error
```

## Q20. Explain Ariba -\> ECC.

``` text
Ariba
 ↓
Managed Gateway
 ↓
Validation / transformation
 ↓
Middleware
 ↓
Cloud Connector
 ↓
ECC
 ↓
IDoc / Proxy / API
 ↓
ECC business processing
```

------------------------------------------------------------------------

# 26. Quick Revision

## Architecture

``` text
ARIBA / NETWORK
      |
      v
MANAGED GATEWAY / CIG
      |
      v
CLOUD INTEGRATION
      |
      v
CLOUD CONNECTOR
      |
      v
ECC
```

## Troubleshooting

``` text
IDENTIFY
   ↓
LOCATE
   ↓
READ ERROR
   ↓
INSPECT PAYLOAD
   ↓
CLASSIFY LAYER
   ↓
FIX ROOT CAUSE
   ↓
REPROCESS SAFELY
   ↓
VERIFY
```

## Five questions

1.  What document?
2.  Which direction?
3.  Where did it fail?
4.  What exact error?
5.  What payload/value caused it?

## Error layers

``` text
Network
Authentication
Authorization
XML
Mapping
Gateway
Middleware
Cloud Connector
ECC Interface
ECC Application
Business Configuration
```

## One-line interview answer

> **PnI is the technical integration layer connecting SAP Ariba and SAP
> Business Network with enterprise systems such as SAP ECC/S/4HANA using
> components and technologies including Managed Gateway/CIG, SAP
> Integration Suite, Cloud Connector, cXML/XML, APIs, IDocs, proxies,
> mappings, authentication, monitoring and error handling.**

------------------------------------------------------------------------

# 27. Official References

Use current SAP Help documentation for release-specific configuration.
Product names, endpoints, supported documents and authentication options
can change.

-   SAP Integration Suite, Managed Gateway for Spend Management and SAP
    Business Network: https://help.sap.com/docs/sisgw

-   Managed Gateway installation guide:
    https://help.sap.com/docs/sisgw/sap-ariba-cloud-integration-gateway-installation-guide

-   Managed Gateway configuration guide:
    https://help.sap.com/docs/sisgw/sap-ariba-cloud-integration-gateway-configuration-guide

-   SAP Integration Suite: https://help.sap.com/docs/integration-suite

-   SAP Cloud Connector:
    https://help.sap.com/docs/connectivity/sap-btp-connectivity-cf/cloud-connector

-   SAP Business Network cXML solutions:
    https://help.sap.com/docs/business-network-for-procurement/cxml-solutions

------------------------------------------------------------------------

## Disclaimer

This is an educational and interview/support reference.

SAP Ariba integration behavior varies by:

-   solution
-   release
-   ECC/S4 release
-   integration scenario
-   customer configuration
-   middleware
-   authentication model
-   mappings
-   business configuration

Do not treat every example as universal SAP behavior.

Never publish customer:

-   payloads
-   credentials
-   certificates/private keys
-   internal endpoints
-   production logs
-   confidential screenshots
-   proprietary implementation documents

Use sanitized/fictitious examples in public repositories.
