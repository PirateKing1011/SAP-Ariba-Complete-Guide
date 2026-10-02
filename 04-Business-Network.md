# SAP Business Network --- Complete Practical Guide

> **Business Network = the collaboration and transaction layer between
> buyers and suppliers.**
>
> This chapter focuses on SAP Business Network, Supplier Collaboration,
> Supplier Connectivity (SCC), purchase orders (PO), order
> confirmations, advance ship notices (ASN), invoices, credit memos,
> cXML documents, transaction flow, document statuses, supplier
> onboarding, and troubleshooting.

------------------------------------------------------------------------

## Table of Contents

1.  What is SAP Business Network?
2.  Business Network Architecture
3.  Buyer, Supplier and Network Roles
4.  SAP Business Network vs Ariba Procurement
5.  SCC --- Supplier Connectivity / Collaboration Concepts
6.  Supplier Onboarding
7.  Trading Relationship
8.  Purchase Order (PO)
9.  PO Document and Lifecycle
10. Order Confirmation
11. Advance Ship Notice (ASN)
12. ASN Document and Lifecycle
13. Goods Receipt
14. Invoice
15. Credit Memo
16. Document and Transaction Flow
17. End-to-End PO → ASN → Receipt → Invoice
18. cXML Business Network Messages
19. PO Payload Example
20. ASN Payload Example
21. Invoice Payload Example
22. Transaction Statuses
23. Document Status vs Transaction Status
24. Supplier Actions
25. Buyer Actions
26. Collaboration Scenarios
27. Partial Shipment
28. Partial Confirmation
29. PO Change / Cancellation
30. Service and Material Scenarios
31. Common Business Network Issues
32. PO Issues
33. Order Confirmation Issues
34. ASN Issues
35. Invoice Issues
36. Supplier Connectivity Issues
37. cXML / Payload Issues
38. Routing Issues
39. Duplicate Transactions
40. Troubleshooting Methodology
41. End-to-End Incident Examples
42. Support Runbook
43. Implementation Checklist
44. Interview Questions
45. Quick Revision
46. Official SAP References
47. Disclaimer

------------------------------------------------------------------------

# 1. What is SAP Business Network?

SAP Business Network is a cloud-based business collaboration network
that connects buyers and suppliers.

A simplified procurement collaboration model is:

``` text
BUYER
  |
  | Purchase Order
  v
SAP BUSINESS NETWORK
  |
  |----------------------|
  |                      |
  v                      v
SUPPLIER              Supplier Systems
  |
  | Order Confirmation
  | ASN
  | Invoice
  v
SAP BUSINESS NETWORK
  |
  v
BUYER
```

The network is not simply an email inbox.

It supports structured business transactions and collaboration between
trading partners.

Typical transactions include:

-   Purchase orders
-   Purchase order changes
-   Order confirmations
-   Advance ship notices
-   Goods receipt information
-   Invoices
-   Credit memos
-   Service-related documents
-   Catalog/content collaboration
-   Supplier collaboration scenarios

Exact document availability depends on the customer's SAP solution,
network relationship and configured scenario.

------------------------------------------------------------------------

# 2. Business Network Architecture

## 2.1 Conceptual architecture

``` text
                    BUYER
              SAP Ariba / ERP
                     |
                     |
                     v
          +----------------------+
          | SAP BUSINESS NETWORK |
          |                      |
          | Trading Relationship |
          | Document Routing     |
          | Transaction Exchange |
          | Supplier Collaboration|
          +----------+-----------+
                     |
             +-------+-------+
             |               |
             v               v
         SUPPLIER       SUPPLIER ERP
         ACCOUNT        / SYSTEM
```

## 2.2 With SAP ECC

``` text
                BUYER ORGANIZATION
                       |
                       v
                  SAP ECC / S4
                       |
                       v
               Ariba / Integration
                       |
                       v
             SAP BUSINESS NETWORK
                       |
             +---------+---------+
             |                   |
             v                   v
        Supplier Portal     Supplier ERP
```

The exact technical route can involve Managed Gateway/CIG, SAP
Integration Suite, APIs, cXML, Cloud Connector, or other configured
integration components.

Refer to the PnI chapter for the technical integration layer.

------------------------------------------------------------------------

# 3. Buyer, Supplier and Network Roles

## Buyer

The buyer creates or receives procurement transactions.

Typical responsibilities:

-   Create PO
-   Send PO
-   Receive confirmation
-   Receive ASN
-   Receive invoice
-   Process receipt
-   Resolve exceptions
-   Manage supplier relationship

## Supplier

The supplier responds to buyer transactions.

Typical actions:

-   Receive PO
-   Confirm PO
-   Reject or partially confirm
-   Create ASN
-   Ship goods
-   Submit invoice
-   Respond to changes

## Network

The network provides the collaboration and transaction exchange layer.

Conceptually:

``` text
Buyer
  |
  v
Network
  |
  v
Supplier
```

------------------------------------------------------------------------

# 4. SAP Business Network vs Ariba Procurement

These concepts are related but should not be treated as identical.

## SAP Ariba Procurement

Focuses on buyer-side procurement activities such as:

``` text
Shopping
PR
Approval
PO
Receiving
Invoice
```

## SAP Business Network

Focuses on buyer-supplier collaboration and transaction exchange:

``` text
PO
Confirmation
ASN
Invoice
Credit Memo
Supplier collaboration
```

## Simple distinction

``` text
P2O:
"What does the buyer need to buy?"

Business Network:
"How do buyer and supplier exchange and collaborate on the transaction?"
```

------------------------------------------------------------------------

# 5. SCC --- Supplier Connectivity / Collaboration Concepts

> **Important:** "SCC" can be used differently across SAP projects and
> documents. Always confirm the exact expansion and scope used by your
> project.

For this repository, SCC is used as a practical umbrella for **supplier
connectivity/collaboration capabilities and processes** around the
network.

Supplier connectivity can involve:

-   Supplier portal/account
-   cXML
-   Integration APIs
-   Supplier ERP integration
-   Email-based routing in supported scenarios
-   Network relationships
-   Supplier enablement
-   Transaction routing

## Supplier connectivity models

A supplier may interact through:

``` text
1. Portal/browser
2. cXML integration
3. Supplier ERP integration
4. API/integration solution
5. Other supported network connectivity
```

Do not assume every supplier uses the same connectivity model.

------------------------------------------------------------------------

# 6. Supplier Onboarding

Supplier onboarding is more than creating a supplier record.

Typical process:

``` text
Identify Supplier
       |
       v
Create / Invite Supplier
       |
       v
Supplier Registers
       |
       v
Trading Relationship
       |
       v
Enable Transactions
       |
       v
Test
       |
       v
Production
```

## Onboarding checklist

-   Supplier identity confirmed
-   Correct supplier account
-   Correct ANID/network identity
-   Trading relationship established
-   Transaction types enabled
-   Routing configured
-   Contact information validated
-   Test transaction completed
-   Production transaction validated

## Common onboarding mistakes

-   Wrong supplier account
-   Wrong ANID
-   Supplier has multiple accounts
-   Relationship not activated
-   Wrong routing configuration
-   Transaction type not enabled
-   Test and production accounts mixed

------------------------------------------------------------------------

# 7. Trading Relationship

A trading relationship defines the collaboration relationship between
buyer and supplier on the network.

Conceptually:

``` text
Buyer Account
      |
      | Trading Relationship
      |
      v
Supplier Account
```

The relationship can determine what transactions are exchanged and under
what configuration.

When a document fails to reach a supplier, verify the trading
relationship before assuming the PO payload is broken.

------------------------------------------------------------------------

# 8. Purchase Order (PO)

A purchase order is a formal buyer request to a supplier to provide
goods or services under specified commercial conditions.

Typical PO data:

-   PO number
-   PO date
-   Buyer
-   Supplier
-   Company code
-   Purchasing organization
-   Currency
-   Payment terms
-   Delivery information
-   Ship-to
-   Bill-to
-   Line items
-   Quantity
-   UOM
-   Price
-   Tax
-   Delivery date
-   Account assignment

------------------------------------------------------------------------

# 9. PO Document and Lifecycle

## 9.1 Conceptual PO lifecycle

``` text
Created
  |
  v
Approved
  |
  v
Sent to Network
  |
  v
Supplier Receives
  |
  +-------> Confirmed
  |
  +-------> Partially Confirmed
  |
  +-------> Rejected
  |
  v
Shipped
  |
  v
Received
  |
  v
Invoiced
  |
  v
Processed / Closed
```

The exact status model varies by application and configuration.

## 9.2 PO line item

A PO can contain multiple lines:

``` text
PO 4500001234

Line 10:
Laptop
Qty = 10

Line 20:
Monitor
Qty = 20

Line 30:
Docking Station
Qty = 10
```

A supplier may confirm or ship lines differently depending on the
supported process.

------------------------------------------------------------------------

# 10. Order Confirmation

An order confirmation is a supplier response to the purchase order.

The supplier can communicate information such as:

-   Accepted quantity
-   Rejected quantity
-   Confirmed delivery date
-   Supplier reference
-   Substitution where supported
-   Pricing differences where supported

Conceptually:

``` text
Buyer
 |
 | PO
 v
Supplier
 |
 | Confirmation
 v
Buyer
```

## Partial confirmation

Example:

``` text
PO:
100 units

Supplier:
Confirmed = 80
Rejected = 20
```

The buyer must evaluate the resulting business status.

------------------------------------------------------------------------

# 11. Advance Ship Notice (ASN)

ASN means **Advance Ship Notice**.

It informs the buyer about a shipment before or around the time goods
are delivered.

Typical ASN information:

-   Shipment number
-   PO reference
-   Supplier
-   Ship-from
-   Ship-to
-   Shipment date
-   Carrier
-   Tracking/reference
-   Packaging
-   Handling units
-   Line items
-   Quantity shipped
-   UOM

## ASN mental model

``` text
PO
 |
 v
Supplier prepares shipment
 |
 v
ASN
 |
 v
Buyer prepares for receipt
 |
 v
Physical delivery
 |
 v
Goods Receipt
```

## ASN vs Goods Receipt

They are not the same.

``` text
ASN:
Supplier says:
"I have shipped these goods."

Goods Receipt:
Buyer records:
"I received these goods."
```

------------------------------------------------------------------------

# 12. ASN Document and Lifecycle

Example:

``` text
PO 4500001234
      |
      v
Supplier ships
      |
      v
ASN 8000012345
      |
      v
Network
      |
      v
Buyer
      |
      v
Warehouse / ERP
      |
      v
Goods Receipt
```

## ASN can contain

``` text
Shipment
  |
  +-- Package
  |     |
  |     +-- Item
  |
  +-- Package
        |
        +-- Item
```

The exact hierarchy depends on the supported document model.

## Partial shipment

PO:

``` text
100 units
```

Shipment 1:

``` text
ASN = 60
```

Shipment 2:

``` text
ASN = 40
```

Total:

``` text
100
```

This is different from one ASN containing 100 units.

------------------------------------------------------------------------

# 13. Goods Receipt

Goods receipt is the buyer-side recording of physically received goods.

Example:

``` text
PO = 100
ASN = 100
Received = 95
```

The buyer may need to investigate the 5-unit difference.

Possible reasons:

-   Short shipment
-   Damage
-   Partial delivery
-   Warehouse counting issue
-   ASN mismatch

## Important distinction

``` text
PO
= what buyer ordered

ASN
= what supplier says was shipped

Receipt
= what buyer says was received
```

This distinction becomes important for invoice reconciliation.

------------------------------------------------------------------------

# 14. Invoice

The supplier submits an invoice requesting payment.

Typical invoice information:

-   Invoice number
-   Invoice date
-   Supplier
-   Buyer
-   PO reference
-   Currency
-   Tax
-   Line items
-   Quantity
-   Price
-   Total
-   Payment terms

Conceptually:

``` text
PO
 |
 v
Shipment
 |
 v
Receipt
 |
 v
Invoice
 |
 v
Reconciliation
 |
 v
Payment
```

------------------------------------------------------------------------

# 15. Credit Memo

A credit memo reduces the amount payable or corrects a previous invoice,
depending on the business scenario.

Example:

``` text
Original invoice:
₹100,000

Credit:
₹10,000

Adjusted amount:
₹90,000
```

A credit memo should not be confused with simply cancelling an invoice.

The exact accounting treatment depends on the backend process.

------------------------------------------------------------------------

# 16. Document and Transaction Flow

## Standard flow

``` text
             PURCHASE ORDER
                    |
                    v
             BUSINESS NETWORK
                    |
                    v
                SUPPLIER
                    |
             +------+------+
             |             |
             v             v
        CONFIRMATION      ASN
             |             |
             +------+------+
                    |
                    v
               GOODS RECEIPT
                    |
                    v
                 INVOICE
                    |
                    v
             RECONCILIATION
                    |
                    v
                 PAYMENT
```

## System flow

``` text
Buyer ERP / Ariba
       |
       v
Integration Layer
       |
       v
Business Network
       |
       v
Supplier
       |
       v
Business Network
       |
       v
Integration Layer
       |
       v
Buyer ERP / Ariba
```

------------------------------------------------------------------------

# 17. End-to-End PO → ASN → Receipt → Invoice

Consider:

``` text
PO = 100 laptops
Price = ₹50,000 each
```

## Step 1 --- PO

Buyer sends:

``` text
Qty = 100
Price = ₹50,000
```

## Step 2 --- Confirmation

Supplier confirms:

``` text
Qty = 100
Delivery = 15 Oct
```

## Step 3 --- ASN

Supplier ships:

``` text
Qty = 60
```

ASN:

``` text
Shipment = 60
```

## Step 4 --- Receipt

Buyer receives:

``` text
Qty = 58
```

## Step 5 --- Invoice

Supplier invoices:

``` text
Qty = 58
```

The buyer's reconciliation process can compare:

``` text
PO quantity
ASN quantity
Receipt quantity
Invoice quantity
```

This is the core business reason why these documents must be traceable.

------------------------------------------------------------------------

# 18. cXML Business Network Messages

Many network integrations use cXML-based business documents.

Conceptually:

``` text
PO
OrderRequest

Confirmation
ConfirmationRequest

ASN
ShipNoticeRequest

Receipt
ReceiptRequest

Invoice
InvoiceDetailRequest
```

Do not memorize names without understanding the business meaning.

A better interview answer is:

``` text
OrderRequest
    = PO message

ConfirmationRequest
    = supplier confirmation

ShipNoticeRequest
    = ASN/shipment notification

ReceiptRequest
    = receipt-related message

InvoiceDetailRequest
    = invoice message
```

Exact usage depends on the configured SAP Business Network scenario.

------------------------------------------------------------------------

# 19. PO Payload Example

Educational example:

``` xml
<?xml version="1.0" encoding="UTF-8"?>

<cXML payloadID="PO-4500001234"
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
            <UserAgent>Example ERP Integration</UserAgent>
        </Sender>
    </Header>

    <Request deploymentMode="production">
        <OrderRequest>

            <OrderRequestHeader
                orderID="4500001234"
                orderDate="2026-10-01T08:30:00Z">

                <Total>
                    <Money currency="INR">500000</Money>
                </Total>

            </OrderRequestHeader>

        </OrderRequest>
    </Request>

</cXML>
```

This is a simplified learning example.

------------------------------------------------------------------------

# 20. ASN Payload Example

Simplified educational example:

``` xml
<cXML payloadID="ASN-8000012345"
      timestamp="2026-10-10T10:00:00Z">

    <Header>
        <From>
            <Credential domain="NetworkID">
                <Identity>SUPPLIER456</Identity>
            </Credential>
        </From>

        <To>
            <Credential domain="NetworkID">
                <Identity>BUYER123</Identity>
            </Credential>
        </To>

        <Sender>
            <Credential domain="NetworkID">
                <Identity>SUPPLIER_SYSTEM</Identity>
            </Credential>
        </Sender>
    </Header>

    <Request>
        <ShipNoticeRequest>

            <ShipNoticeHeader
                shipmentID="ASN-8000012345"
                shipmentDate="2026-10-10T10:00:00Z" />

            <ShipControl>
                <CarrierIdentifier>
                    <Contact>
                        Example Carrier
                    </Contact>
                </CarrierIdentifier>
            </ShipControl>

        </ShipNoticeRequest>
    </Request>

</cXML>
```

Production payloads are more detailed and scenario-specific.

------------------------------------------------------------------------

# 21. Invoice Payload Example

Simplified:

``` xml
<cXML payloadID="INV-9000012345"
      timestamp="2026-10-15T10:00:00Z">

    <Header>
        <From>
            <Credential domain="NetworkID">
                <Identity>SUPPLIER456</Identity>
            </Credential>
        </From>

        <To>
            <Credential domain="NetworkID">
                <Identity>BUYER123</Identity>
            </Credential>
        </To>
    </Header>

    <Request>
        <InvoiceDetailRequest>

            <InvoiceDetailRequestHeader
                invoiceID="INV-9000012345"
                invoiceDate="2026-10-15" />

        </InvoiceDetailRequest>

    </Request>
</cXML>
```

Again, this is educational rather than a complete production invoice
schema.

------------------------------------------------------------------------

# 22. Transaction Statuses

Statuses can exist at several levels.

Examples include:

``` text
Created
Sent
Acknowledged
Confirmed
Rejected
Shipped
Received
Invoiced
Processed
Failed
```

Do not assume every document supports every status.

## Technical status vs business status

A technical transaction may say:

``` text
Successfully delivered
```

while the business document can still be rejected later.

Example:

``` text
Network delivery = SUCCESS

Supplier business action = REJECTED
```

Therefore always distinguish:

``` text
Technical delivery
vs
Business processing
```

------------------------------------------------------------------------

# 23. Document Status vs Transaction Status

This distinction is extremely important.

## Transaction status

Answers:

> Did the message technically process?

Example:

``` text
COMPLETED
FAILED
RETRY
```

## Business document status

Answers:

> What is the business state of the PO/invoice/ASN?

Example:

``` text
Confirmed
Rejected
Shipped
Received
Invoiced
```

A transaction can be technically successful while the business document
has a business exception.

------------------------------------------------------------------------

# 24. Supplier Actions

Typical supplier workflow:

``` text
Receive PO
   |
   v
Review
   |
   +----> Reject
   |
   +----> Confirm
             |
             v
          Prepare
             |
             v
           Ship
             |
             v
           ASN
             |
             v
          Invoice
```

Supplier responsibilities include:

-   Reviewing PO
-   Confirming accurate quantities
-   Communicating exceptions
-   Creating ASN
-   Providing shipment information
-   Submitting invoice
-   Maintaining network connectivity

------------------------------------------------------------------------

# 25. Buyer Actions

Typical buyer workflow:

``` text
Create PO
   |
   v
Send
   |
   v
Monitor confirmation
   |
   v
Monitor ASN
   |
   v
Receive goods
   |
   v
Reconcile invoice
   |
   v
Approve/payment process
```

Buyer support teams should be able to trace the entire chain.

------------------------------------------------------------------------

# 26. Collaboration Scenarios

## Scenario A --- Full confirmation

``` text
PO = 100
Confirmation = 100
ASN = 100
Receipt = 100
Invoice = 100
```

Straightforward flow.

## Scenario B --- Partial confirmation

``` text
PO = 100
Confirmation = 80
```

Buyer needs to understand why 20 are not confirmed.

## Scenario C --- Partial shipment

``` text
PO = 100

ASN 1 = 60
ASN 2 = 40
```

Total shipped = 100.

## Scenario D --- Short receipt

``` text
PO = 100
ASN = 100
Receipt = 95
```

Potential exception.

## Scenario E --- Invoice mismatch

``` text
PO = 100
Receipt = 95
Invoice = 100
```

The reconciliation process may create a quantity exception depending on
configured tolerances.

------------------------------------------------------------------------

# 27. Partial Shipment

Partial shipments are common in real procurement.

Example:

``` text
PO:
100 monitors

Supplier shipment:
40

ASN:
40

Remaining:
60
```

Later:

``` text
ASN:
60

Total:
100
```

Support should check:

-   PO quantity
-   confirmation
-   ASN quantity
-   received quantity
-   remaining open quantity

------------------------------------------------------------------------

# 28. Partial Confirmation

Example:

``` text
PO = 100

Supplier confirms:
70

Supplier cannot supply:
30
```

Questions:

-   Was the rejection intentional?
-   Is the buyer expecting another confirmation?
-   Is a replacement/alternative needed?
-   Does the buyer need a new PO?

The exact business handling depends on procurement policy.

------------------------------------------------------------------------

# 29. PO Change / Cancellation

A buyer may change:

-   quantity
-   delivery date
-   price
-   address
-   line item
-   other supported fields

A PO change should be treated as a business transaction, not simply as
an updated screen value.

Conceptually:

``` text
Original PO
    |
    v
Change
    |
    v
PO Change Message
    |
    v
Network
    |
    v
Supplier
```

## Cancellation

``` text
PO
 |
 v
Cancellation
 |
 v
Network
 |
 v
Supplier
```

Before cancelling or changing a PO, check its current business state and
supplier response.

------------------------------------------------------------------------

# 30. Service and Material Scenarios

## Material

Usually involves:

``` text
Material
Quantity
UOM
Price
Delivery
Receipt
```

## Service

May involve:

``` text
Service description
Quantity / units
Value
Service entry
Approval
Invoice
```

Service processes can differ substantially from material procurement.

Do not apply material ASN/receipt assumptions blindly to every service
scenario.

------------------------------------------------------------------------

# 31. Common Business Network Issues

Classify issues first.

``` text
Supplier account
Trading relationship
Routing
PO
Confirmation
ASN
Receipt
Invoice
cXML
Authentication
Integration
Duplicate
Business configuration
```

------------------------------------------------------------------------

# 32. PO Issues

## Issue 1 --- PO not received by supplier

Check:

1.  Was PO created?
2.  Was it approved?
3.  Was it sent?
4.  Did transaction reach Business Network?
5.  Is supplier relationship active?
6.  Is supplier account correct?
7.  Is routing correct?
8.  Does supplier see the document?

## Issue 2 --- Wrong supplier

Possible causes:

-   incorrect supplier master
-   wrong network ID
-   incorrect trading relationship
-   wrong routing

## Issue 3 --- PO rejected

Determine whether:

``` text
Technical rejection
```

or:

``` text
Supplier/business rejection
```

These require different investigations.

## Issue 4 --- PO duplicate

Check:

-   PO number
-   network transaction ID
-   supplier reference
-   resend history
-   retry history

------------------------------------------------------------------------

# 33. Order Confirmation Issues

## Confirmation not visible

Check:

``` text
Supplier submitted?
       |
       v
Network received?
       |
       v
Buyer relationship?
       |
       v
Integration?
       |
       v
Buyer system?
```

## Confirmation quantity mismatch

Example:

``` text
PO = 100
Confirmation = 80
```

Check whether supplier intentionally confirmed only 80.

## Wrong delivery date

Check:

-   supplier confirmation
-   buyer expected date
-   PO change
-   timezone/date interpretation
-   integration mapping

------------------------------------------------------------------------

# 34. ASN Issues

## ASN not received

Check:

-   Supplier generated ASN?
-   ASN transmitted?
-   PO reference correct?
-   Supplier relationship active?
-   cXML valid?
-   Network accepted?
-   Buyer integration received?
-   ECC interface processed?

## ASN quantity mismatch

Example:

``` text
PO = 100
ASN = 120
```

Possible reasons:

-   supplier error
-   over-shipment
-   duplicate ASN
-   wrong line mapping
-   unit-of-measure conversion

Do not assume it is always a technical defect.

## ASN references wrong PO

This is usually a data/reference issue.

Trace:

``` text
Supplier system
  |
ASN payload
  |
PO reference
  |
Network
```

------------------------------------------------------------------------

# 35. Invoice Issues

## Invoice not visible

Check:

``` text
Supplier
 |
Network
 |
Gateway
 |
Middleware
 |
ECC/Ariba
```

## Invoice rejected

Possible reasons:

-   invalid PO
-   invalid supplier
-   quantity mismatch
-   price mismatch
-   tax issue
-   currency mismatch
-   missing mandatory field
-   duplicate invoice
-   business rule

## Duplicate invoice

Check:

-   invoice number
-   supplier
-   invoice date
-   PO
-   transaction ID

Do not simply resend.

------------------------------------------------------------------------

# 36. Supplier Connectivity Issues

## Portal supplier

Possible issues:

-   login
-   account
-   relationship
-   notification
-   document visibility

## cXML supplier

Possible issues:

-   endpoint
-   certificate
-   credentials
-   payload
-   routing
-   network connectivity

## ERP-integrated supplier

Possible issues:

``` text
Supplier ERP
 |
Middleware
 |
Network
```

Trace each layer.

------------------------------------------------------------------------

# 37. cXML / Payload Issues

Common problems:

### Missing mandatory data

``` text
PO number missing
Supplier ID missing
Currency missing
```

### Wrong sender/receiver

``` text
From = wrong supplier
To = wrong buyer
```

### Invalid reference

``` text
ASN references non-existent PO
```

### Invalid quantity

``` text
Quantity = -10
```

### Wrong UOM

``` text
EA vs BOX
```

### Invalid date

``` text
Unexpected date format
```

### Malformed XML

Unclosed tags, invalid characters or namespace problems.

------------------------------------------------------------------------

# 38. Routing Issues

Routing determines where a document should go.

Conceptually:

``` text
Document
   |
   v
Identify Receiver
   |
   v
Trading Relationship
   |
   v
Routing Configuration
   |
   v
Supplier
```

If a PO reaches the network but not the supplier, investigate routing.

Possible causes:

-   wrong receiver
-   wrong network ID
-   relationship missing
-   supplier account mismatch
-   transaction type not enabled
-   routing rule/configuration

------------------------------------------------------------------------

# 39. Duplicate Transactions

Duplicates can be dangerous.

Possible causes:

-   manual resend
-   automatic retry
-   timeout followed by resend
-   duplicate source event
-   supplier resend
-   integration replay

Before retrying:

``` text
Did target receive it?
Did target create a document?
Did supplier receive it?
Is there already an invoice/ASN?
```

Never use "resend" as the first troubleshooting step.

------------------------------------------------------------------------

# 40. Troubleshooting Methodology

## Step 1 --- Collect evidence

Always get:

``` text
Environment
Buyer
Supplier
Document type
Document number
Transaction ID
Timestamp
Exact error
```

## Step 2 --- Identify business document

``` text
PO?
Confirmation?
ASN?
Invoice?
Credit memo?
```

## Step 3 --- Determine direction

``` text
Buyer -> Supplier
Supplier -> Buyer
```

## Step 4 --- Determine technical path

``` text
Portal?
cXML?
API?
Gateway?
Middleware?
ERP?
```

## Step 5 --- Search transaction

Find:

``` text
Transaction
Status
Payload
Error
Sender
Receiver
```

## Step 6 --- Analyze payload

Check:

-   IDs
-   sender
-   receiver
-   references
-   quantities
-   UOM
-   currency
-   dates

## Step 7 --- Classify error

``` text
Connectivity
Authentication
Routing
Payload
Mapping
Network
ERP
Business
```

## Step 8 --- Fix root cause

## Step 9 --- Reprocess safely

## Step 10 --- Verify business result

------------------------------------------------------------------------

# 41. End-to-End Incident Examples

## Incident 1 --- PO not received

User:

> Supplier says they did not receive PO 4500001234.

Investigation:

``` text
1. Verify PO exists
2. Verify PO was approved
3. Verify PO was sent
4. Search network transaction
5. Check receiver
6. Check trading relationship
7. Check supplier account
8. Check routing
9. Check supplier visibility
```

### Possible root cause

Wrong supplier network ID.

### Lesson

A missing supplier PO is not automatically a payload problem.

------------------------------------------------------------------------

## Incident 2 --- ASN not visible to buyer

Supplier says:

> ASN 8000012345 was submitted.

Check:

``` text
Supplier submission
       |
Network transaction
       |
PO reference
       |
Buyer integration
       |
Buyer ERP
```

If network accepted it but buyer ERP did not process it:

``` text
Investigate integration/ECC
```

------------------------------------------------------------------------

## Incident 3 --- Invoice rejected

Invoice:

``` text
INV-900001
PO = 4500001234
Qty = 100
```

Receipt:

``` text
Qty = 80
```

Possible result:

``` text
Quantity exception
```

Do not immediately call it a CIG failure.

This may be a business reconciliation issue.

------------------------------------------------------------------------

## Incident 4 --- ASN quantity greater than PO

``` text
PO = 100
ASN = 120
```

Possible causes:

-   supplier over-shipment
-   wrong line
-   wrong UOM
-   duplicate ASN
-   source-system error

Investigate payload and business context before correcting data.

------------------------------------------------------------------------

## Incident 5 --- Supplier sees wrong PO quantity

Buyer:

``` text
PO = 100
```

Supplier sees:

``` text
PO = 10
```

Trace:

``` text
Buyer source
 |
payload
 |
mapping/transformation
 |
Network
 |
supplier display
```

If payload itself contains 10, investigate upstream.

If payload contains 100 but supplier displays 10, investigate downstream
processing/rendering.

------------------------------------------------------------------------

# 42. Support Runbook

## Ticket template

``` text
Environment:
TEST / PROD

Buyer:

Supplier:

Supplier Network ID:

Document Type:

Document Number:

Transaction ID:

Date/Time:

Sender:

Receiver:

Error:

Expected Result:

Actual Result:
```

## Investigation

### Buyer

-   Document created?
-   Approved?
-   Sent?

### Network

-   Transaction found?
-   Status?
-   Receiver?
-   Payload?
-   Error?

### Supplier

-   Relationship active?
-   Document visible?
-   Supplier action completed?

### Integration

-   Gateway?
-   Middleware?
-   Cloud Connector?
-   API/cXML?
-   ECC?

### Resolution

-   Root cause
-   Fix
-   Reprocess
-   Duplicate risk
-   Verification

------------------------------------------------------------------------

# 43. Implementation Checklist

## Network

-   [ ] Buyer account
-   [ ] Supplier account
-   [ ] Trading relationship
-   [ ] Supplier network ID
-   [ ] Transaction types
-   [ ] Routing

## PO

-   [ ] PO transmission
-   [ ] Supplier receipt
-   [ ] PO response
-   [ ] PO change
-   [ ] PO cancellation

## Confirmation

-   [ ] Full confirmation
-   [ ] Partial confirmation
-   [ ] Rejection

## ASN

-   [ ] ASN creation
-   [ ] PO reference
-   [ ] Shipment quantity
-   [ ] Carrier information
-   [ ] Partial shipment
-   [ ] Multiple shipments

## Receipt

-   [ ] Goods receipt
-   [ ] Partial receipt
-   [ ] Over/short receipt
-   [ ] Receipt integration

## Invoice

-   [ ] Invoice submission
-   [ ] PO reference
-   [ ] Quantity matching
-   [ ] Price matching
-   [ ] Tax
-   [ ] Duplicate detection
-   [ ] Credit memo

## Testing

-   [ ] Happy path
-   [ ] Partial confirmation
-   [ ] Partial shipment
-   [ ] Partial receipt
-   [ ] Invoice mismatch
-   [ ] Invalid PO
-   [ ] Invalid supplier
-   [ ] Duplicate transaction
-   [ ] Routing failure
-   [ ] cXML error
-   [ ] Integration failure

------------------------------------------------------------------------

# 44. Interview Questions

## Q1. What is SAP Business Network?

It is a cloud-based network for buyer-supplier collaboration and
exchange of structured business transactions.

## Q2. What is the difference between Ariba Procurement and Business Network?

Ariba Procurement primarily supports buyer procurement processes, while
Business Network enables buyer-supplier collaboration and exchange of
transactions.

## Q3. What is an ASN?

ASN means Advance Ship Notice. It communicates shipment information from
supplier to buyer before/around delivery.

## Q4. ASN vs Goods Receipt?

ASN is supplier-side shipment information. Goods receipt is buyer-side
confirmation of physical receipt.

## Q5. What is OrderRequest?

In cXML-based scenarios, OrderRequest commonly represents a purchase
order message.

## Q6. What is ShipNoticeRequest?

It commonly represents shipment/ASN information.

## Q7. What is InvoiceDetailRequest?

It commonly represents invoice information.

## Q8. PO vs ASN?

``` text
PO = Buyer orders
ASN = Supplier says what was shipped
```

## Q9. ASN vs Invoice?

``` text
ASN = Shipment
Invoice = Payment request
```

## Q10. Why can a PO reach Network but not supplier?

Possible reasons include:

-   trading relationship
-   routing
-   supplier account
-   receiver identity
-   transaction enablement
-   supplier connectivity

## Q11. Why can ASN be accepted but not appear in ERP?

The network may have accepted it while downstream integration or ERP
processing failed.

## Q12. What do you check for a missing PO?

``` text
PO created
PO approved
PO sent
Network transaction
Receiver
Trading relationship
Routing
Supplier account
Supplier visibility
```

## Q13. What causes duplicate transactions?

Retries, manual resends, timeouts, source-system duplicates or replay.

## Q14. What is partial shipment?

Supplier ships less than the total PO quantity and may send multiple
ASNs until the order is fulfilled.

## Q15. What is a trading relationship?

The buyer-supplier relationship that enables configured collaboration
and transaction exchange on the network.

## Q16. What is supplier enablement?

Preparing and configuring a supplier to participate in network
transactions through an appropriate connectivity model.

## Q17. How would you troubleshoot an ASN failure?

I would collect the ASN and PO numbers, identify the supplier and
environment, locate the network transaction, inspect the payload and PO
reference, identify the failure layer, check downstream integration if
the network accepted the ASN, correct the root cause and reprocess only
after checking duplicate risk.

## Q18. How do you troubleshoot an invoice mismatch?

Compare:

``` text
PO
Confirmation
ASN
Receipt
Invoice
```

Then identify whether the mismatch is quantity, price, tax, currency,
supplier, reference or configuration-related.

## Q19. What is the most important identifier?

There is no single universal identifier. I would correlate using the
business document number, transaction ID/payload ID, supplier identity
and timestamps.

## Q20. Explain PO → ASN → Receipt → Invoice.

``` text
PO
Buyer orders

ASN
Supplier reports shipment

Receipt
Buyer records receipt

Invoice
Supplier requests payment

Reconciliation
Buyer validates the invoice
```

------------------------------------------------------------------------

# 45. Quick Revision

## Business Network

``` text
BUYER
  |
  v
BUSINESS NETWORK
  |
  v
SUPPLIER
```

## Core documents

``` text
PO
 ↓
Confirmation
 ↓
ASN
 ↓
Receipt
 ↓
Invoice
 ↓
Payment
```

## Key distinctions

``` text
PO
= What buyer ordered

Confirmation
= What supplier accepts

ASN
= What supplier shipped

Receipt
= What buyer received

Invoice
= What supplier requests payment for
```

## Technical vs business

``` text
Technical:
Did the message travel?

Business:
Did the transaction make sense?
```

## Troubleshooting

``` text
IDENTIFY
 ↓
LOCATE
 ↓
PAYLOAD
 ↓
ROUTING
 ↓
CONNECTIVITY
 ↓
BUSINESS VALIDATION
 ↓
FIX
 ↓
REPROCESS
 ↓
VERIFY
```

------------------------------------------------------------------------

# 46. Official SAP References

Use current SAP Help documentation for release-specific behavior and
configuration.

-   SAP Business Network: https://help.sap.com/docs/business-network

-   SAP Business Network for Procurement:
    https://help.sap.com/docs/business-network-for-procurement

-   SAP Business Network for Supply Chain:
    https://help.sap.com/docs/business-network-for-supply-chain

-   SAP Integration Suite, managed gateway for spend management and SAP
    Business Network: https://help.sap.com/docs/sisgw

-   SAP Business Network cXML solutions:
    https://help.sap.com/docs/business-network-for-procurement/cxml-solutions

------------------------------------------------------------------------

# 47. Disclaimer

This guide is an educational, implementation, support and interview
reference.

SAP Business Network capabilities, document types, statuses, routing
options, supplier connectivity methods and integration behavior can vary
by:

-   SAP solution
-   Release
-   Subscription
-   Trading-partner configuration
-   Customer configuration
-   Integration architecture
-   Supplier connectivity method
-   Backend system

Examples in this repository are simplified or fictional unless
explicitly stated otherwise.

Never publish:

-   Customer payloads
-   Production screenshots
-   Credentials
-   Certificates/private keys
-   Internal endpoints
-   Supplier confidential data
-   Customer-specific configuration

Use sanitized examples for public documentation.

------------------------------------------------------------------------

# Final Learning Checklist

You should be able to explain:

-   [ ] SAP Business Network
-   [ ] Buyer vs supplier role
-   [ ] Trading relationship
-   [ ] Supplier onboarding
-   [ ] Supplier connectivity
-   [ ] SCC concepts
-   [ ] PO
-   [ ] PO lifecycle
-   [ ] Order confirmation
-   [ ] Partial confirmation
-   [ ] ASN
-   [ ] Partial shipment
-   [ ] Goods receipt
-   [ ] Invoice
-   [ ] Credit memo
-   [ ] cXML
-   [ ] OrderRequest
-   [ ] ConfirmationRequest
-   [ ] ShipNoticeRequest
-   [ ] ReceiptRequest
-   [ ] InvoiceDetailRequest
-   [ ] Transaction status
-   [ ] Document status
-   [ ] Routing
-   [ ] Supplier enablement
-   [ ] Duplicate transactions
-   [ ] Network troubleshooting
-   [ ] Payload analysis
-   [ ] PO issues
-   [ ] ASN issues
-   [ ] Invoice issues
-   [ ] End-to-end transaction tracing

## One-line interview summary

> **SAP Business Network provides the collaboration and transaction
> layer connecting buyers and suppliers, allowing documents such as
> purchase orders, confirmations, ASNs, receipts, invoices and credit
> memos to be exchanged through configured trading relationships and
> connectivity mechanisms.**
