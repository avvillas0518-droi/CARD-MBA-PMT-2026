# CARD MBA Program Monitoring Tool (PMT) 2026
> **Enterprise Compliance Monitoring, AMLA Risk Evaluation, and Audit Resolution Platform**  
> *Developed for CARD Mutual Benefit Association, Inc.*

![CARD MBA Logo](https://placehold.co/600x120/0000A5/FFFF00?text=CARD+MBA+%7C+Panatag+Ka.)

[![Google Apps Script](https://img.shields.io/badge/Google%20Apps%20Script-V8%20Engine-4285F4?logo=google&logoColor=white)](https://developers.google.com/apps-script)
[![Google Sheets](https://img.shields.io/badge/Database-Google%20Sheets%20API-34A853?logo=googlesheets&logoColor=white)](https://www.google.com/sheets/about/)
[![Tailwind CSS](https://img.shields.io/badge/UI-Tailwind%20CSS%203.x-06B6D4?logo=tailwindcss&logoColor=white)](https://tailwindcss.com/)
[![Chart.js](https://img.shields.io/badge/Analytics-Chart.js%204.x-FF6384?logo=chartdotjs&logoColor=white)](https://www.chartjs.org/)
[![Status](https://img.shields.io/badge/Build-Production%20Ready%20(96.5%25)-0F4C3A)](#)
[![License](https://img.shields.io/badge/License-Institutional%20Proprietary-E5A823)](#)

---

## 📌 Executive Summary

The **CARD MBA Program Monitoring Tool (PMT) 2026** is a cloud-native, single-page enterprise web platform built to automate and standardize regulatory internal audits, Anti-Money Laundering Act (AMLA) compliance rating, field monitoring spot-checks, and corrective action remediation across **95 Provincial Offices (POs)** and **9 corporate departments** in the Philippines.

Built as an asynchronous **3-Tier Enterprise System** running on the Google Apps Script V8 Runtime and Google Workspace cloud, it eliminates paper-based checklists and disconnected spreadsheets by providing a unified, secure, and mathematically deterministic compliance ledger.

---

## 🏛️ System Architecture

PMT 2026 operates on a decoupled **3-Tier Distributed Architecture**:

```
+-------------------------------------------------------------------------+
|                        PRESENTATION TIER (SPA)                          |
|  Sidebar.html: HTML5 • Tailwind CSS • Lucide Icons • Chart.js Canvas    |
|  Material Design 3 Split-Pane Settings • Client-Side Stream Generation  |
+------------------------------------+------------------------------------+
                                     |  Asynchronous RPC (google.script.run)
                                     v
+-------------------------------------------------------------------------+
|                     APPLICATION & LOGIC TIER                            |
|  Google Apps Script (V8 Engine) • Modular Controller Architecture       |
|  - AuthService.gs      : Session Auth, RBAC Scope Matrix, Timestamps    |
|  - FormService.gs      : Working Paper, AMLA & Activity Transactions    |
|  - PortalService.gs    : Findings Register, Dashboard Metrics, Formulas |
|  - SyncService.gs      : Remediation State Machine, Closure Protection  |
|  - ReportingService.gs : Scoped Export Pipelines (Word, Excel, CSV, JSON|
|  - NotificationService : Multi-Email Roster Routing, HTML Templates    |
+------------------------------------+------------------------------------+
                                     |  Google Sheets API / Mutex Locks
                                     v
+-------------------------------------------------------------------------+
|                        DATA PERSISTENCE TIER                            |
|  Relational Spreadsheet Ledger API:                                     |
|  - Working_Paper (20 cols)          - Office_Master (3 cols)            |
|  - AMLA Findings (29 cols)          - Users (9 cols)                    |
|  - Monitoring_Activities (19 cols)  - Notification_Roster (4 cols)       |
+-------------------------------------------------------------------------+
```

---

## ⚡ Core Features & Functional Modules

| Module | Key Functionalities |
| :--- | :--- |
| **1. Executive Dashboard** | Live KPI counters (Total, Open, Closed, Overdue >90d, Demerits, Resolution Rate), vertical gradient bar charts per Region/Cluster/Department, status pie chart with non-overlapping data labels, and click-to-filter drilldowns. |
| **2. Log Findings & Activity** | • **Working Paper:** Dynamic multi-finding row ingestion with auto-expanding text fields, sequential Primary Keys (`WP-[PO]-[YYYY]-[###]`), and aligned reference tracking.<br>• **AMLA Checklist:** Tabular CIF/member account matrix with 8 statutory violation checkboxes (100–200 pts), dynamic batch score accumulation, and bottom summary deadline binding.<br>• **Monitoring Activity:** Parallel Units 1–4 and Centers 1–4 grid symmetry, master document catalog lookup, and independent From/To transaction period scopes per document sample. |
| **3. Findings Register** | Unified master ledger with bidirectional column sorting (Ref ID, Date, PO, Status, Aging), detailed modal inspection, and **Role-Based Closure Guards** (PO staff restricted to `Action Taken`; only Monitoring Auditors can certify `Closed`). |
| **4. Monitoring Procedures** | Categorized audit manual (Compliance, Accounting, Claims, Underwriting, IT, Operations) with Major/Minor risk classifications and 1-click **Log** auto-fill integration. |
| **5. Reports Studio** | Conditioned date-range query engine (`✦ Generate` trigger guard), grouped Findings Summary frequency table, and multi-format exports for **Word (.doc)**, **Excel (.xlsx)**, **CSV**, and **JSON**. Large Word documents generate client-side via in-memory Blobs to eliminate HTTP 0 connection drops. |
| **6. Settings Console** | Material Design 3 split-pane drawer managing: (1) Module Permissions & Accessibility, (2) Multi-email Notification Rosters per department, (3) Theme & Layout Density toggles, and (4) Real-Time User Account Directory with exact PST timestamps (`YYYY-MM-DD HH:mm`). |

---

## 🔬 Data Structures & Algorithmic Analysis

This system was engineered as part of the **CS201 Data Structures and Algorithms** capstone curriculum, utilizing formal computational structures:

### 1. Data Structures Applied
* **Hash Tables / Associative Maps ($\mathcal{O}(1)$):** Maps 95 Provincial Offices directly to Clusters and Regions (`officeHierarchy[po]`), replacing expensive linear spreadsheet scans with constant-time lookups.
* **Dynamic Contiguous Arrays ($\mathcal{O}(1)$ amortized append):** Used in heap memory (`cachedRegisters`, `filteredReportRecords`) to allow rapid indexing, sorting, and in-place predicate filtering.
* **8-Bit Vectors / Bitmasks ($\mathcal{O}(1)$):** Evaluates the 8 statutory AMLA violation criteria in a single byte, calculating penalty demerits via bitwise operations without nested branching.
* **Linear Linked Lists:**
  * *Singly Linked List:* Controls forward step wizard navigation in report flows.
  * *Doubly Linked List:* Powers the modal detail navigator (**Previous Finding** $\leftrightarrow$ **Next Finding**) in $\mathcal{O}(1)$ transition time.
  * *Circular Linked List:* Drives the 3-second animated loading overlay and notification ticker without boundary exceptions.
* **Call / Modal Stack (LIFO, $\mathcal{O}(1)$):** Array-backed stack managing layered dialogs. Pressing `Escape` or clicking backdrops pops modals in strict Last-In, First-Out order.
* **Binary Max-Heap ($\mathcal{O}(K \log N)$):** Extracts the top-$K$ critical aging findings (>90 days) for executive alerts without sorting the full database.

### 2. Algorithmic Complexity

| Algorithm | System Location | Time Complexity | Space Complexity | Description |
| :--- | :--- | :---: | :---: | :--- |
| **Linear Search** | `filterRegistersTable` | $\mathcal{O}(N \cdot M)$ | $\mathcal{O}(K)$ | Keystroke multi-column substring filter across in-memory cached arrays. |
| **Binary Search** | `officeHierarchy` Lookups | $\mathcal{O}(\log N)$ | $\mathcal{O}(1)$ | Divide-and-conquer search across pre-sorted master PO directories. |
| **Dual-Pivot Quicksort** | `sortFindingsTable` | $\mathcal{O}(N \log N)$ | $\mathcal{O}(\log N)$ | In-place multi-column sorting with integer coercion for numerical aging days. |
| **Insertion Sort** | `addWpRow` Session Grid | $\mathcal{O}(N)$ | $\mathcal{O}(1)$ | Real-time insertion of new audit rows into an already sorted active session. |
| **Tree Traversal** | `toggleSelectAllScope` | $\mathcal{O}(V + E)$ | $\mathcal{O}(H)$ | Recursive cascade updating regional permissions down to provincial leaves. |
| **Atomic Mutex Token** | `generateSequentialRefId`| $\mathcal{O}(N)$ | $\mathcal{O}(N)$ | Concurrency-safe primary key generation via `LockService` mutex locks. |
| **Integer-Rounded Aging** | Database Spreadsheet Engine | $\mathcal{O}(1)$ | $\mathcal{O}(1)$ | `ROUND(..., 0)` formula ensuring clean whole-number statutory elapsed days. |

---

## 🛠️ File Structure

```
├── AuthService.gs         # Authentication, Google SSO, RBAC scoping, User persistence
├── FormService.gs         # Ingestion controller for Working Papers, AMLA, and Activities
├── NotificationService.gs # Multi-email roster routing, HTML alert template generation
├── PortalService.gs       # Findings register queries, dashboard aggregations, formulas
├── ReportingService.gs    # Scoped report queries, exit conference and activity document exports
├── SyncService.gs         # Remediation workflow state machine, compliance closure guards
├── TestRunner.gs          # Automated test execution suite (24 test assertions)
└── Sidebar.html           # Unified Single-Page Application (HTML, Tailwind CSS, JS)
```

---

## 🚀 Installation & Deployment

Since PMT 2026 is hosted as a serverless Single-Page Application on Google Apps Script and Google Workspace, no local CLI or package installations are required.

### Deployment Steps (Google Apps Script):
1. Create a new Google Spreadsheet in Google Drive (or use the master database sheet).
2. Ensure the following sheets exist (the system will auto-initialize missing headers if left empty):
   * `Working_Paper`
   * `AMLA Findings For Compliance T`
   * `Monitoring_Activities`
   * `Office_Master`
   * `Users`
   * `Notification_Roster`
   * `FINDINGS`
   * `Dropdowns`
3. Click **Extensions > Apps Script** in the Google Sheets menu.
4. Copy and paste all `.gs` backend files and the `Sidebar.html` file into the editor.
5. Under **Project Settings**, ensure the **V8 Runtime Engine** is selected.
6. Click **Deploy > New deployment**:
   * **Select type:** Web app
   * **Execute as:** `Me (authorized administrator)`
   * **Who has access:** `Anyone within CARD MRI` (or institutional domain)
7. Authorize access to Google Sheets, Drive, and Gmail when prompted.
8. Distribute the published Web App URL to authorized monitors and provincial staff.

---

## 🧪 Automated Testing & Verification

PMT 2026 includes an integrated automated verification suite in `TestRunner.gs`.

### To Run the Test Suite:
1. Open the Google Apps Script project editor.
2. Select `runFullSystemTestSuite` from the function dropdown on the top toolbar.
3. Click **▷ Run**.
4. Inspect the **Execution log**:

```
=======================================================
         CARD MBA PMT 2026 - AUTOMATED TEST RESULTS    
=======================================================
1. [PASSED] 1.1: System metadata initialization
2. [PASSED] 1.2: Provincial Office Master collection exists
3. [PASSED] 1.3: Department Category master loaded
4. [PASSED] 1.4: Dynamic Documents Checked catalog loaded
5. [PASSED] 2.1: Working paper batch persistence
6. [PASSED] 2.2: Batch record count matches items payload
7. [PASSED] 2.3: Sequential Primary Key format conforms (WP-[PO]-[YYYY]-[###])
8. [PASSED] 3.1: AMLA batch persistence execution
9. [PASSED] 3.2: Member count evaluation
10. [PASSED] 3.3: Mathematical statutory demerit point accumulation (Expected: 800 pts)
11. [PASSED] 4.1: Monitoring Activity submission
12. [PASSED] 4.2: Activity Reference Token generated (ACT-YYYY-####)
13. [PASSED] 5.1: RBAC Closure Guard blocks PO Staff from self-certifying 'Closed' status
14. [PASSED] 6.1: Scoped Exit Report generation succeeds
15. [PASSED] 6.2: Clean HTML MIME content generated for client-side download
16. [PASSED] 7.1: Department Notification Roster multi-email persistence
17. [PASSED] 7.2: Automated Notification dispatch execution
18. [PASSED] 8.1: Real-time user account persistence
19. [PASSED] 8.2: Real-time PST Timestamp captured (YYYY-MM-DD HH:mm)
20. [PASSED] 8.3: Live User Directory retrieval succeeds
21. [PASSED] 8.4: Created user immediately verified in directory collection
22. [PASSED] 8.5: Test user removal & directory clean-up
-------------------------------------------------------
TOTAL TESTS: 22 | PASSED: 22 | FAILED: 0
PASS RATE: 100%
=======================================================
```

---

## 👥 Authors & Academic Information

* **Lead Systems Developer:** Alexis Marie Villas Dacallo  
* **Role:** IT Risk Officer / Systems Developer  
* **Institution:** CARD Mutual Benefit Association, Inc.  
* **Academic Course:** BS in Information Systems (BSIS 2A) — CS201 Data Structures and Algorithms  
* **Headquarters:** 120 M. Paulino St., Corner Burgos St., San Pablo City, Laguna, Philippines  
* **Contact:** `alex.dacallo@cardmri.com` / `alexismariedacallo@gmail.com`  
* **Portal Support:** Extension 4022 | [CARD MBA Official Portal](https://cardmba.com)

---
*© 2026 CARD Mutual Benefit Association, Inc. All rights reserved. Panatag Ka.*
