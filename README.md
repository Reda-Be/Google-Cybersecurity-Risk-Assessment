# 🛡️ Risk Analysis & Network Hardening

> **📝 Note:** This project is a practical exercise from the **Google Cybersecurity** Professional Certificate on Coursera. It is a simulation based on a fictional company.

## 📖 Project Scenario
As a cybersecurity analyst for a social media organization, I responded to a **major data breach** (leak of customer names and addresses). The objective was to identify the root causes of the breach and propose a remediation plan based on modern standards.

### 🔍 Detected Vulnerabilities
The network audit revealed four critical flaws:
1. **Password Sharing:** Poor digital hygiene practices among employees.
2. **Default Credentials:** The database admin password had never been changed.
3. **Lack of Filtering:** The firewall had no active rules to block suspicious traffic.
4. **Weak Authentication:** Absence of Multi-Factor Authentication (MFA).

---

## 🚀 Security Strategy (Hardening)
To address these flaws, I developed a strategy based on the **Zero Trust Architecture (ZTA)** and **NIST SP 800-41** standards:

* **Identity Management (Zero Trust Principle):**
    * **"Never trust, always verify":** Implementation of **mandatory MFA** for all access, both internal and external.
    * Enforcement of a password policy compliant with **NIST** recommendations.
    * Immediate removal of all **default credentials** to prevent unauthorized lateral movement.

* **Network Security & Micro-segmentation:**
    * **Firewall Hardening:** Configuration of rules following the **"Deny by Default"** policy to reduce the attack surface.
    
    #### 🛠️ Firewall Configuration (NIST Principle):
    * **Policy:** Deny by Default.
    * **Action:** Closing insecure ports 21 (FTP) and 23 (Telnet). Opening port 443 (HTTPS) only for incoming Web traffic.
    * **Filtering:** Restricting database access (Port 3306) solely to the Application Server's IP address.

    <details>
    <summary>📄 Click to view configuration commands (Linux UFW)</summary>

    ```bash
    # 1. Default policy: block all incoming traffic
    ufw default deny incoming
    ufw default allow outgoing

    # 2. Explicitly close dangerous unencrypted protocols
    ufw deny 21/tcp
    ufw deny 23/tcp

    # 3. Open secure Web (HTTPS) for public access
    ufw allow 443/tcp

    # 4. Database Security (MariaDB/MySQL)
    # Allow ONLY the specific IP address of the application server
    ufw allow from 192.168.1.50 to any port 3306
    ```
    </details>

    #### 🛠️ SQL Management (Principle of Least Privilege):
    * **Action:** Discontinued use of the `root` account for daily tasks.
    * **Implementation:** Creation of restricted user accounts in MariaDB/MySQL.
    * **Example Command:** `GRANT SELECT, INSERT ON db.* TO 'user'@'ip';`
    * **Objectif:** Prevent accidental or malicious data deletion (Drop/Delete) by limiting permissions to the bare minimum.
    * **Application of the Principle of Least Privilege (PoLP):** Users access only the resources strictly necessary for their role.

* **Governance & Awareness:**
    * Implementation of mandatory monthly training to establish a security culture and stop credential sharing.

---

## 🛠️ Demonstrated Skills
* **Risk Analysis:** Threat identification and remediation prioritization.
* **Modern Frameworks:** Application of **Zero Trust** principles and **NIST** guidelines.
* **Attack Surface Reduction:** Technical configuration and system hardening.
* **Database Security:** SQL privilege management and access security.

---
*Project completed to validate network security skills for the Google Cybersecurity Professional Certificate.*
