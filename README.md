## Enterprise Identity Governance & Zero Trust Architecture


<a href="https://github.com/InformationSecurityEngineerr/Identity-and-Access-Management/tree/main?tab=readme-ov-file#technical-implementation-details">Phase 1: Identity Governance & Attribute-Based Access Control (ABAC)</a>
(Completed) ████████████████████ 100%

Focus: Automated Identity Lifecycle Management, Dynamic Membership Rules, and UPN standardization.

Phase 2: Adaptive Security & Conditional Access Policy Design 
(In Progress) ▓▓░░░░░░░░░░░░░░░░░░ 10%

---

### *Identity Governance & Attribute-Based Access Control (ABAC)*

In this phase, I established a cloud-native identity foundation using **Microsoft Entra ID**. The primary objective was to transition from manual user management to **Attribute-Based Access Control (ABAC)**. This ensures that as users move through an organization—via onboarding, transfers, or offboarding—their access is automatically provisioned and revoked, adhering to the principle of **Least Privilege**.

---

### *Technical Implementation Details*

#### 1. Identity Architecture & Persona Creation

I provisioned a dedicated Microsoft 365 Developer tenant (`micrlabs.onmicrosoft.com`) to simulate a corporate environment.

* **Standardized Naming Conventions:** Implemented professional UPNs, such as `Sec.Analyst` and `Sales.User`, to reflect industry identity standards.
* **Security Best Practice:** Renamed the default administrator to `Global.Admin` as part of a "Break-Glass" account strategy.
* **Attribute Enrichment:** Populated specific metadata fields (Job Title, Department) for each persona to drive downstream automation.

#### 2. Automated Group Membership (Dynamic Groups)

Instead of manual assignments, I utilized **Dynamic Membership Rules** to automate group entry based on user metadata.

* **Group Created:** `SG-Sales-Dynamic`.
* **Rule Logic:** `(user.department -eq "Sales")`.
* **Significance:** This eliminates human error in granting access. When a user is hired into a department, they receive necessary permissions immediately without manual administrative intervention.

#### 3. Identity Lifecycle Simulation (Onboarding & Transfers)

I simulated an "Internal Transfer" scenario to test the robustness of the automated logic:

* **The Action:** Updated a user's `Department` attribute from **Sales** to **Marketing**.
* **The Outcome:** The Entra ID polling engine detected the change, simultaneously revoking access to Sales resources while granting access to Marketing resources.
* **Security Benefit:** This effectively mitigates **"Privilege Creep,"** where employees retain access to old departments after changing roles.

---

### *Validation & Auditing*

Validation was performed by monitoring the **Entra ID Audit Logs**.

* **System Integrity:** The logs confirm that membership changes were initiated by the **"Core Directory"** (system), proving the automation logic functions correctly without manual interference.
* **Audit Evidence:** Captured the specific "Add member" and "Remove member" events triggered by the attribute change.

---

### *Key Takeaways*

> During the group creation phase, I opted not to make this a role-assignable group. This decision was made to support **Dynamic Membership**, ensuring that users are automatically offboarded or onboarded based on their 'Department' attribute in Entra ID, rather than requiring manual administrative intervention.

**Phase 1 Complete** | *Proceeding to Phase 2: Adaptive Security & Conditional Access Policy Design*
