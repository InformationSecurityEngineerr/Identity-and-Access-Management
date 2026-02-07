## Enterprise Identity Governance & Zero Trust Architecture
![Azure](https://img.shields.io/badge/azure-%230072C6.svg?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Microsoft Entra ID](https://img.shields.io/badge/Microsoft%20Entra%20ID-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Zero Trust](https://img.shields.io/badge/Zero%20Trust-Security-blueviolet?style=for-the-badge)
### 📑 Project Navigation

<a href="https://github.com/InformationSecurityEngineerr/Identity-and-Access-Management/edit/main/README.md#identity-governance--attribute-based-access-control-abac">Phase 1: Identity Governance & Attribute-Based Access Control (ABAC)</a>

Focus: Automated Identity Lifecycle Management, Dynamic Membership Rules, and UPN standardization.
---

### *Identity Governance & Attribute-Based Access Control (ABAC)*

In this phase, I established a cloud-native identity foundation using **Microsoft Entra ID**. The primary objective was to transition from manual user management to **Attribute-Based Access Control (ABAC)**. This ensures that as users move through an organization—via onboarding, transfers, or offboarding—their access is automatically provisioned and revoked, adhering to the principle of **Least Privilege**.

---

### *Technical Implementation Details*

#### 1. Identity Architecture & Persona Creation

I provisioned a dedicated Microsoft 365 Developer tenant (`micrlabs.onmicrosoft.com`) to simulate a corporate environment.

**Standardized Naming Conventions:** Implemented professional UPNs, such as `Sec.Analyst` and `Sales.Analyst`, to reflect industry identity standards.
<img width="3071" height="852" alt="image" src="https://github.com/user-attachments/assets/ea8b186c-8678-4f0d-b5e7-68343d9ff8b6" />
* **Security Best Practice:** Renamed the default administrator to `Global.Admin` as part of a "Break-Glass" account strategy.
<img width="2191" height="1083" alt="image" src="https://github.com/user-attachments/assets/4713ee02-8ced-4fe1-8605-90d55237f1da" />
**Attribute Enrichment:** Populated specific metadata fields (Job Title, Department) for each persona to drive downstream automation.
<img width="3065" height="1202" alt="image" src="https://github.com/user-attachments/assets/62b8c8d6-c576-489a-a78b-cd7cdd0bd7e4" />



#### 2. Automated Group Membership (Dynamic Groups)

Instead of manual assignments, I utilized **Dynamic Membership Rules** to automate group entry based on user metadata.

**Group Created:** `SG-Sales-Dynamic`.
<img width="3071" height="1158" alt="image" src="https://github.com/user-attachments/assets/25061d6c-353f-4163-9ff5-7c265e22bc04" />
**Rule Logic:** `(user.department -eq "Sales")`.
<img width="3071" height="945" alt="image" src="https://github.com/user-attachments/assets/3b3c9914-8c2c-46f9-b46b-dd0595363c95" />

**Significance:** This eliminates human error in granting access. When a user is hired into a department, they receive necessary permissions immediately without manual administrative intervention.

#### 3. Identity Lifecycle Simulation (Onboarding & Transfers)

I simulated an "Internal Transfer" scenario to test the robustness of the automated logic:

**The Action:** Updated a user's `Department` attribute from **Sales** to **Marketing**.
<img width="2292" height="1302" alt="image" src="https://github.com/user-attachments/assets/2eab90d6-8a74-4232-aeec-0b953fb113fa" />

**The Outcome:** The Entra ID polling engine detected the change, simultaneously revoking access to Sales resources while granting access to Marketing resources.
**Security Benefit:** This effectively mitigates **"Privilege Creep,"** where employees retain access to old departments after changing roles.

---

### *Validation & Auditing*

Validation was performed by monitoring the **Entra ID Audit Logs**.

**System Integrity:** The logs confirm that membership changes were initiated by the **"Core Directory"** (system), proving the automation logic functions correctly without manual interference.
<img width="3071" height="1317" alt="image" src="https://github.com/user-attachments/assets/aae492b6-a5f2-4de5-b9cc-d645cf525e80" />

**Audit Evidence:** Captured the specific "Add member" and "Remove member" events triggered by the attribute change.

---

### *Key Takeaways*

> [!IMPORTANT]
> **Architectural Decision:** During the group creation phase, I opted not to make this a role-assignable group. This supports **Dynamic Membership**, ensuring that users are automatically offboarded or onboarded based on their 'Department' attribute without manual intervention.
<img width="2365" height="1007" alt="image" src="https://github.com/user-attachments/assets/cc14eb17-a607-415a-89e6-28ebbb807ee8" />


**Phase 1 Complete** | *Proceeding to Phase 2: Adaptive Security & Conditional Access Policy Design*


