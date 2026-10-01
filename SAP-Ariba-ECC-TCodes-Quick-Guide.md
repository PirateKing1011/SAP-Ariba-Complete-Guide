# SAP Ariba – SAP ECC/S/4HANA T-Code Quick Guide

A short practical cheat sheet for the most commonly used SAP transactions when working with **SAP Ariba / SAP Business Network integrations**.

> **Important:** Exact transactions and usage can vary by ECC/S/4HANA version, integration design, and installed SAP Ariba/Managed Gateway components. `CIG` is the commonly used historical/project term; SAP's current product name is **SAP Integration Suite, managed gateway for spend management and SAP Business Network**.

---

## 1. Most-Used Integration & Troubleshooting T-Codes

| T-Code | Simple meaning | When you use it | Typical Ariba flow |
|---|---|---|---|
| **SLG1** | Application Log | First place to check application/interface logs | Ariba/Managed Gateway → ECC → **SLG1** |
| **WE02** | Display IDocs | Check IDoc status, segments and errors | Ariba/Network ↔ Gateway → ECC → **WE02** |
| **BD87** | IDoc Reprocessing | Reprocess failed IDocs after fixing the root cause | **WE02** → Fix issue → **BD87** |
| **SRT_MONI** | Web Service Monitor | Monitor/analyze SOAP/web-service messages | Ariba → Gateway → Web Service → **SRT_MONI** |
| **SM58** | tRFC Monitor | Check failed transactional RFC calls | ECC → RFC → **SM58** |
| **SM59** | RFC Destinations | Check/test RFC connection configuration | ECC ↔ Middleware → **SM59** |
| **SM37** | Background Jobs | Check scheduled/background jobs and job logs | Job → Processing → **SM37** |
| **ST22** | ABAP Dumps | Check runtime errors/short dumps | Transaction → ABAP error → **ST22** |
| **SM21** | System Log | Check system-level errors/events | System → Error → **SM21** |
| **SU53** | Authorization Check | Identify missing SAP authorizations | User action → Authorization error → **SU53** |
| **WE20** | Partner Profiles | Check IDoc partner configuration | IDoc setup → Partner → **WE20** |
| **WE19** | IDoc Test Tool | Test/create IDocs in a controlled test scenario | Test IDoc → Process → **WE19** |
| **SPRO** | SAP Customizing | Configure SAP/Ariba integration settings | Configuration → **SPRO** |
| **/IWFND/ERROR_LOG** | Gateway Error Log | Analyze SAP Gateway/OData errors | OData/API → Error → **/IWFND/ERROR_LOG** |

---

## 2. The Most Important Ones — Remember These First

| Priority | T-Code | Remember it as |
|---|---|---|
| ⭐⭐⭐⭐⭐ | **SLG1** | Application/interface logs |
| ⭐⭐⭐⭐⭐ | **WE02** | Check IDoc |
| ⭐⭐⭐⭐⭐ | **BD87** | Reprocess IDoc |
| ⭐⭐⭐⭐ | **SRT_MONI** | Web-service monitoring |
| ⭐⭐⭐⭐ | **SM37** | Background jobs |
| ⭐⭐⭐⭐ | **ST22** | ABAP dump |
| ⭐⭐⭐ | **SM58** | Failed tRFC |
| ⭐⭐⭐ | **SM59** | RFC connection |
| ⭐⭐⭐ | **WE20** | IDoc partner profile |
| ⭐⭐⭐ | **SPRO** | Configuration |
| ⭐⭐⭐ | **SU53** | Authorization problem |
| ⭐⭐ | **SM21** | System log |
| ⭐⭐ | **WE19** | IDoc testing |

---

## 3. Practical Ariba Support Flow

### A. General Integration Failure

```text
Transaction fails
      ↓
Check SAP Ariba / Business Network
      ↓
Check Managed Gateway / Transaction Tracker
      ↓
Check ECC
      ↓
SLG1
      ↓
WE02 / SRT_MONI
      ↓
Classify the error
      ↓
Fix root cause
      ↓
Reprocess if appropriate
      ↓
BD87 / relevant reprocessing mechanism
      ↓
Verify end-to-end status
```

---

### B. IDoc Failure

```text
Ariba / Network
      ↓
Managed Gateway
      ↓
ECC
      ↓
WE02
      ↓
Check IDoc status + error
      ↓
Fix master/configuration/data issue
      ↓
BD87
      ↓
Recheck WE02
```

**Example:** IDoc has an error because required master data is missing.

`WE02 → read error → fix master data → BD87 → verify successful status`

SAP's Managed Gateway documentation explicitly uses `WE02` to view IDoc errors and `BD87` is the standard SAP IDoc status/reprocessing tool. 

---

### C. Application Log Failure

```text
Ariba transaction
      ↓
ECC processing
      ↓
SLG1
      ↓
Object / Subobject
      ↓
Read message
      ↓
Identify root cause
```

For Managed Gateway integrations, SAP documentation specifically references `SLG1` with objects such as `ARBCIG_INTERFACE` / subobject `IF_LOGS` for interface logs. Exact objects vary by process. 

---

### D. Web-Service Failure

```text
Ariba
   ↓
Managed Gateway / Middleware
   ↓
Web Service
   ↓
ECC
   ↓
SRT_MONI
   ↓
Check request / response / error
```

Use this particularly when the integration uses SAP web services/proxies rather than an IDoc-based path.

---

## 4. Business Document T-Codes

These are not specifically "Ariba monitoring" transactions. They are useful when checking the actual SAP business document involved in an Ariba transaction.

| T-Code | Business document | Simple use |
|---|---|---|
| **ME53N** | Purchase Requisition | Display PR |
| **ME52N** | Purchase Requisition | Change PR |
| **ME51N** | Purchase Requisition | Create PR |
| **ME23N** | Purchase Order | Display PO |
| **ME22N** | Purchase Order | Change PO |
| **ME21N** | Purchase Order | Create PO |
| **MIGO** | Goods Movement | Goods receipt / material movement |
| **MIRO** | Invoice | Enter/post invoice |
| **MIR4** | Invoice | Display invoice document |
| **FB03** | Accounting Document | Display FI accounting document |

---

## 5. Simple End-to-End Examples

### Example 1 — PO was created but not sent

```text
PO created in ECC
      ↓
ME23N
      ↓
Check PO
      ↓
Check output/integration processing
      ↓
SLG1
      ↓
WE02 / SRT_MONI
      ↓
Managed Gateway / middleware
      ↓
Business Network
```

---

### Example 2 — Supplier document failed in ECC

```text
Business Network
      ↓
Managed Gateway
      ↓
ECC
      ↓
WE02
      ↓
IDoc error
      ↓
Fix issue
      ↓
BD87
      ↓
Successful processing
```

---

### Example 3 — Invoice problem

```text
Supplier invoice
      ↓
Business Network
      ↓
Managed Gateway
      ↓
ECC
      ↓
SLG1 / WE02 / SRT_MONI
      ↓
Invoice processing
      ↓
MIRO / MIR4 / FI document
      ↓
Reconciliation / accounting check
```

---

## 6. Quick "Which T-Code Do I Open?" Table

| Problem | Start with |
|---|---|
| "Something failed in the Ariba integration" | **SLG1** |
| "Where is the IDoc?" | **WE02** |
| "IDoc failed; can I reprocess it?" | **BD87** |
| "Web-service message failed" | **SRT_MONI** |
| "RFC call failed" | **SM58** |
| "Is the RFC destination working?" | **SM59** |
| "Background job failed?" | **SM37** |
| "SAP generated a dump" | **ST22** |
| "System-level error?" | **SM21** |
| "Authorization error?" | **SU53** |
| "IDoc partner configuration?" | **WE20** |
| "Need to test an IDoc?" | **WE19** |
| "Need SAP integration configuration?" | **SPRO** |
| "Check PR?" | **ME53N** |
| "Check PO?" | **ME23N** |
| "Check goods receipt?" | **MIGO** |
| "Check invoice?" | **MIR4** |
| "Check FI accounting document?" | **FB03** |

---

## 7. Interview Revision — One Line Each

- **SLG1** → Application log / interface log analysis.
- **WE02** → Display and analyze IDocs.
- **BD87** → Reprocess IDocs after resolving the cause.
- **SRT_MONI** → Monitor/analyze web-service messages.
- **SM58** → Monitor failed tRFC transactions.
- **SM59** → Maintain/test RFC destinations.
- **SM37** → Monitor background jobs.
- **ST22** → Analyze ABAP short dumps.
- **SM21** → Analyze SAP system log.
- **SU53** → Analyze authorization failures.
- **WE20** → Configure/check IDoc partner profiles.
- **WE19** → Test IDoc processing.
- **SPRO** → SAP configuration/customizing.
- **ME23N** → Display purchase order.
- **ME53N** → Display purchase requisition.
- **MIGO** → Goods movement / receipt.
- **MIR4** → Display invoice.
- **FB03** → Display accounting document.

---

## 8. Golden Support Rule

Do **not** immediately assume:

> "CIG/Managed Gateway issue."

Instead:

```text
Where did the document stop?
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
ECC web service?
        ↓
IDoc?
        ↓
ABAP/application processing?
        ↓
Business/master-data validation?
```

Then use the appropriate monitoring transaction.

---

### Official SAP references

- SAP Managed Gateway documentation: https://help.sap.com/docs/sisgw
- SAP documentation specifically references `SLG1` for Managed Gateway interface logs and `WE02` for IDoc errors. 
