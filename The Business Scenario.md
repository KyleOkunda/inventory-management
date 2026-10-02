


### The Business Scenario

To analyze the exposure, we construct a standard Kenyan FMCG distribution model.

* **Scenario assumption:** A hypothetical FMCG distributor operating a central warehouse in Nairobi, supplying retailers, supermarkets, and wholesalers via a fleet of delivery vans.
* **Operating model:** Sales representatives take orders, the warehouse picks the goods, and drivers execute daily delivery routes.
* **Stock handled:** High-velocity consumer goods tracked in cartons/batches.
* **Current recording methods:** The warehouse uses paper bin cards for physical storage. The finance team uses an off-the-shelf accounting system. Dispatch is managed via paper gate passes.
* **Exception handling:** Drivers report customer returns, damaged goods, or delivery shortages via phone calls or WhatsApp messages to the warehouse manager.

---

### The Stock Lifecycle

Inventory must be analyzed as a continuous lifecycle, not a static number. In this operational model, stock physically moves through the following stages:

```text
Supplier
 ↓
Receiving & Verification
 ↓
Warehouse Storage (Bin Location)
 ↓
Order Picking
 ↓
Dispatch / Truck Loading
 ↓
In-Transit Stock
 ↓
Customer Delivery & Verification
 ↓
Proof of Delivery (POD)
 ↓
Returns / Damaged Goods Handover
 ↓
Stock Reconciliation & Replenishment

```

At every arrow in this diagram, custody of the physical asset changes hands. If the digital record does not update simultaneously with the physical handover, exposure is created.


---

### Where Stock Leakage Exposure Appears

When stock moves without a rigid control mechanism, the business is exposed to multiple points of leakage.

**1. Receiving Discrepancies**

* **Exposure:** A supplier delivers 950 cartons, but the warehouse clerk signs the delivery note for 1,000 cartons.
* **Why it happens:** The receiving bay is busy, and the clerk assumes the paperwork is correct without conducting a blind physical count.
* **Consequence:** The business pays for 50 cartons it never received, and the warehouse inherits an immediate, hidden stock variance.

**2. Truck Loading Discrepancies**

* **Exposure:** A driver is scheduled to take 200 cartons on their route, but 205 are loaded onto the van.
* **Why it happens:** Manual picking errors combined with a lack of a secondary verification check at the loading bay.
* **Consequence:** The extra 5 cartons are no longer tracked by the warehouse system. The driver can sell them off-book, or they may be lost/damaged without any record.

**3. Unrecorded Customer Returns**

* **Exposure:** A customer rejects 2 cartons due to water damage. The driver brings them back to the depot but does not formally hand them over to the storekeeper.
* **Why it happens:** Returns are communicated via WhatsApp; the physical cartons are left in the corner of the loading bay and eventually discarded or misplaced.
* **Consequence:** The system believes the customer kept the goods, creating a billing dispute, while the warehouse loses visibility of the damaged stock.

**4. Unauthorized Manual Adjustments**

* **Exposure:** During a Friday stock count, a storekeeper notices the system says 50 cartons, but only 48 are on the shelf. They edit the spreadsheet to "48" so the numbers match.
* **Why it happens:** Spreadsheets lack role-based access controls and audit trails.
* **Consequence:** The missing 2 cartons are written off silently. Management is never alerted to the leakage, and the root cause is never investigated.

---

### The Leakage Mechanism

Leakage thrives in the gap between a physical action and its digital record. Consider this chain of events:

```text
Warehouse system shows 500 cartons available
 ↓
Paper order dictates 100 cartons to be loaded on Van A
 ↓
Storekeeper physically picks 100 cartons
 ↓
Driver departs and delivers 90 cartons to the customer
 ↓
Customer rejects 10 cartons because they are close to expiry
 ↓
Driver texts the warehouse manager: "Returning 10 cartons."
 ↓
Driver arrives late; leaves the 10 cartons in the parked van overnight
 ↓
The next morning, Van A is loaded for a different route
 ↓
The 10 returned cartons mix with the new dispatch
 ↓
System still expects those 10 cartons to be in the main warehouse
 ↓
Physical count occurs two weeks later
 ↓
Warehouse is short 10 cartons; management assumes theft

```

The control failed because the *Return* transition was recorded via an informal text message rather than an accountable system transaction that updated the stock's location state from "Customer" to "Transit" to "Warehouse Quarantine".

---

### Control-Point Analysis

Every meaningful physical transition requires a corresponding control and evidence record.

| Stock Transition | Risk | Required Control | Evidence |
| --- | --- | --- | --- |
| **Supplier → Warehouse** | Quantity/Quality mismatch | Blind receipt verification against PO (Purchase Order) | Digitally signed GRN (Good Received Note) |
| **Warehouse → Vehicle** | Loading overage/shortage | Gate-pass validation before dispatch | Dispatch confirmation |
| **Vehicle → Customer** | Delivery shortage / Dispute | Customer sign-off at drop point | Digital Proof of Delivery |
| **Customer → Vehicle** | Unrecorded rejection/return | Immediate return logging on mobile app | Return receipt |
| **Vehicle → Warehouse** | Returns disappearing at depot | Formal handover of returned/unsold stock | Depot return log |
| **Warehouse → Damaged** | Unauthorized write-offs | Managerial approval for stock quarantine | Adjustment approval |


---

### Business Impact

When inventory exposure is not tightly controlled, the consequences ripple across the organization.

**Financial exposure**

* **Direct margin erosion:** Unbilled deliveries and lost stock directly reduce net profit.
* **Working capital drain:** Management orders replacement stock for items that are technically in the building but lost in the system (e.g., misplaced in quarantine).

**Operational exposure**

* **Phantom stock-outs:** The system shows 0 units available, halting sales, while physical cartons sit unrecorded in a returned-goods pile.
* **Inefficient dispatch:** Loading bays bottleneck because staff spend hours recounting vans to resolve paper-based loading disputes.

**Customer exposure**

* **Short deliveries:** Customers receive incomplete orders because the warehouse picking list was based on inaccurate system stock.
* **Billing disputes:** Invoicing a customer for 100 cartons when they formally rejected 10 damages trust and delays payment.

**Management exposure**

* **Unreliable visibility:** Management cannot trust the inventory valuation on the balance sheet.
* **Delayed detection:** By the time a quarterly physical count identifies a variance, it is impossible to reconstruct what happened three months ago.

**Control exposure**

* **Shared accountability:** When a discrepancy is found, the storekeeper blames the driver, the driver blames the customer, and the lack of an audit trail means no one can be held responsible.

---

### What Should Be Digitized?

Digitization should target the gaps where physical handoffs occur.

| Activity | Current Method | Exposure | Digital Control Opportunity |
| --- | --- | --- | --- |
| **Receiving** | Paper delivery notes | Blind signing; supplier shortages missed | Mobile GRN matched strictly to Purchase Order |
| **Dispatch** | Verbal counts | Over/under loading vans | Digital pick-list with mandatory dispatch sign-off |
| **Deliveries** | Paper invoices | Lost paperwork; unrecorded returns | Driver web app for POD and real-time return logging |
| **Returns** | Text / Memory | Stock abandoned in depot | Workflow forcing driver to hand back stock to warehouse |
| **Counts** | Excel overwrites | Hiding variances silently | System-guided counts resulting in variance reports |
| **Adjustments** | Direct spreadsheet edits | Unauthorized write-offs | Formal adjustment workflow requiring manager PIN |

---

### The Risk → Control → System Model

Biashara Code Labs maps software capabilities directly to operational risks.

> **Risk:** A supplier delivers fewer cartons than stated on the invoice, but the warehouse clerk signs for the full amount.
> **Control:** The receiving clerk must perform a "blind count" where the system does not show the expected quantity until the physical count is entered.
> **System:** Mobile receiving module + variance detection engine.

> **Risk:** Stock is loaded onto a delivery vehicle, but the driver claims the warehouse shorted them.
> **Control:** Both the picker and the driver must digitally sign off on the exact loaded quantity before the gate pass is generated.
> **System:** Dispatch module + dual user-authentication handoff + digital gate pass.

> **Risk:** A customer rejects damaged goods, and the driver leaves them in the van unrecorded.
> **Control:** The driver must log the exact reason for non-delivery at the customer site, which automatically updates the vehicle's "return stock" ledger.
> **System:** Driver mobile application + real-time state change (Dispatched → Returned).

> **Risk:** Returned goods are dropped at the warehouse but mixed back into sellable stock without quality checks.
> **Control:** Returned stock must be systematically forced into a "Quarantine" location until inspected.
> **System:** Multi-location inventory ledger + automated quarantine routing.

> **Risk:** A storekeeper overwrites a stock shortage in the spreadsheet to avoid getting in trouble.
> **Control:** Prevent manual overriding of the core ledger; variances must be processed as formal "Adjustments."
> **System:** Role-Based Access Control (RBAC) + immutable transaction ledger.

> **Risk:** A branch transfer departs the central warehouse but never arrives at the regional depot.
> **Control:** The system must track inventory as "In-Transit" and trigger an alert if the receiving branch does not confirm receipt within 24 hours.
> **System:** Transfer workflow + aging alerts for unconfirmed receipts.

> **Risk:** Expired goods are quietly thrown away without management knowing the financial value lost.
> **Control:** All write-offs must be quantified and digitally authorized by the Finance Manager before the stock balance decreases.
> **System:** Adjustment approval workflow + financial variance reporting.



---

### Stock States & Ownership

Treating inventory as a single number (e.g., "We have 10,000 units") is operationally dangerous. If a customer calls for 5,000 units, the sales team might promise delivery, only to discover the stock is unavailable.

A mature system models stock by its physical location and state:

* **Warehouse (Sellable):** 7,000
* **Allocated (Picked for pending orders):** 800
* **In-Transit (On delivery vans):** 1,200
* **Quarantine (Pending inspection):** 600
* **Damaged (Pending write-off):** 400

This location-aware visibility ensures that sales reps only sell what is physically in the warehouse, while management can clearly see stock that is currently tied up in delivery vehicles.

---

### Physical Counts & Reconciliation

Even with perfect software, physical stock checks remain mandatory. However, the system mechanics of a stock count must be strictly controlled.

A physical count should **never** simply overwrite the system balance. The proper workflow is:

1. **System Expectation:** The system expects 500 units.
2. **Blind Physical Count:** The team counts and inputs 480 units.
3. **Variance Generation:** The system highlights a -20 variance.
4. **Investigation:** The warehouse manager reviews pending dispatches and recent returns.
5. **Authorized Adjustment:** A senior manager reviews the KES 50,000 loss and inputs their PIN to authorize the write-down.

This ensures that the ledger remains pristine and every discrepancy is explicitly acknowledged by management.

---

### Exception Handling

When physical reality disagrees with the digital record, the system must handle the exception gracefully without stopping operations.

If a driver returns to the depot with 5 cartons, but the system shows the driver delivered everything, the system should not automatically inject 5 phantom cartons into the warehouse. Instead, it should:

1. Flag the discrepancy as an **Unexplained Overage**.
2. Route the 5 physical cartons into a digital "Holding" bucket.
3. Create an investigation task for the inventory controller to review the driver's delivery logs for that day.
4. Require an authorized resolution (e.g., reversing an incorrect customer POD) before the 5 cartons can be recognized as sellable stock again.

Silent, automated corrections destroy data integrity.

---

### Preventive vs Detective Controls

A resilient inventory architecture utilizes two layers of control.

**Preventive Controls** (Stopping leakage before it happens):

* Mandatory dual-sign-off for truck loading.
* Preventing sales orders from processing if the system shows negative stock.
* Restricting "Adjustment" privileges to the Operations Manager.
* Preventing a driver from clearing their daily route log until all returned stock is checked back into the depot.

**Detective Controls** (Identifying leakage after it occurs):

* Daily variance reports highlighting any mismatch between system and physical counts.
* Aging reports for stock sitting in "Quarantine" for more than 7 days.
* Alerts for delivery vehicles that have been "In-Transit" for more than 24 hours.

---

### Inventory Audit Trail

When a discrepancy is found, management must be able to answer: *"What happened to this stock?"*

A properly engineered system maintains an immutable audit trail for every single movement, recording:

* **What:** SKU and quantity.
* **From/To:** Source location and destination location.
* **Who:** The user logged in during the transaction.
* **When:** Exact system timestamp.
* **Why:** The reference document (e.g., Order #4092 or Transfer #88).
* **Evidence:** Signatures, PODs, or adjustment justifications.

This eliminates reliance on memory, text histories, and guesswork during reconciliation.


---

### Management Dashboard

Management does not need to see every transaction; they need to see exceptions. An effective dashboard should highlight:

* **Current Stock by Location:** Value of stock in the warehouse vs. on the road.
* **Unresolved Discrepancies:** The number and value of stock variances awaiting investigation.
* **Quarantined Stock Value:** Capital tied up in damaged or returned goods awaiting processing.
* **Pending Transfers:** Stock dispatched to a branch but not yet received.
* **Stock-Out Warnings:** Fast-moving items approaching minimum reorder levels.

Every metric should prompt an operational question or action.

---

### Alerts & Escalation

To prevent exceptions from aging into permanent losses, the system should trigger automated escalations for specific events:

* **Negative stock positions:** Triggered instantly if inventory line drops below zero.
* **High-value adjustments:** Any manual stock write-off exceeding a predefined threshold (e.g., KES 10,000) requires a senior manager's digital approval.
* **Unconfirmed dispatches:** An alert if a delivery van remains in a "Dispatched" state past the end of the working day without a completed route reconciliation.

---

### What the System Does NOT Solve

To maintain operational realism, it is critical to acknowledge the boundaries of software.

* **Software cannot physically count stock:** If a team blindly inputs "500" during a physical count without actually checking the bins, the system will accept the lie.
* **Collusion:** If a driver and a storekeeper conspire and manipulate the loading documents together, the system will record a valid transaction. (However, the audit trail ensures that their names are permanently attached to that specific movement).
* **Bad Master Data:** If units of measure are set up incorrectly (e.g., confusing pieces with cartons), the software will generate massive, compounding errors.

Software enforces workflows, guarantees traceability, and makes variances immediately visible. It does not replace the need for physical warehouse discipline and management oversight.