# Terms of Use — Sentinel Foundry

**Effective Date:** 1 May 2026  
**Operated by:** Kiranlab UK  
**Contact:** Via the GitHub repository

---

## 1. Acceptance of Terms

By connecting to or using the Sentinel Foundry MCP server (hosted at `mcp.kiranlab.co.uk`), you agree to these Terms of Use. If you do not agree, do not use the service.

---

## 2. Intellectual Property

The Sentinel Foundry project — including all source code, documentation, tool definitions, reasoning logic, and associated materials — is the intellectual property of **Kiranlab UK**.

The source code is made available under the [MIT License](LICENSE). This licence covers the right to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software, subject to the conditions stated in the licence file.

The name **Sentinel Foundry**, the **Kiranlab** brand, and associated logos are trademarks of Kiranlab UK. You may not use these names or marks to imply endorsement of derived products or services without prior written permission.

---

## 3. Third-Party Services

Sentinel Foundry communicates with the following Microsoft Azure services on your behalf using your credentials:

- Microsoft Sentinel API
- Azure Log Analytics API
- Azure Resource Manager API
- Microsoft Graph API (optional, for Defender XDR)

Your use of these APIs is subject to:

- [Microsoft Azure Terms of Service](https://azure.microsoft.com/en-us/support/legal/)
- [Microsoft Privacy Statement](https://privacy.microsoft.com/en-us/privacystatement)
- Your organisation's Azure subscription agreement

Kiranlab UK is not affiliated with, endorsed by, or a representative of Microsoft Corporation. **Microsoft Sentinel**, **Azure**, **Microsoft Copilot**, and related product names are trademarks of Microsoft Corporation.

---

## 4. No Warranty

THE SOFTWARE AND HOSTED SERVICE ARE PROVIDED **"AS IS"**, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AND NON-INFRINGEMENT.

Kiranlab UK does not warrant that:
- The service will be uninterrupted, error-free, or available at all times
- Cost estimates, security scores, detection recommendations, or any other outputs are accurate, complete, or suitable for any specific purpose
- The service will meet your compliance or regulatory requirements

---

## 5. Limitation of Liability

TO THE MAXIMUM EXTENT PERMITTED BY APPLICABLE LAW, KIRANLAB UK SHALL NOT BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, CONSEQUENTIAL, OR PUNITIVE DAMAGES ARISING FROM:

- Your use of or inability to use the service
- Any security decisions, configuration changes, or actions taken based on outputs from this service
- Inaccurate cost estimates, security scores, or recommendations
- Unauthorised access to your Azure environment

**You are solely responsible for:** validating all outputs before acting on them, ensuring your Azure RBAC is configured appropriately, and complying with your organisation's security policies.

---

## 6. Data Handling

Sentinel Foundry is designed with a **zero-retention** architecture:

- **No workspace data is stored** on Kiranlab UK infrastructure beyond the duration of your active session
- **No query results, log samples, or schema information** are persisted to disk or databases
- **Your Azure credentials** (tokens) are used only within your session to authenticate API calls and are never written to storage
- **Access logs** (IP address, endpoint, timestamp) may be retained by the web server for up to 90 days for security and abuse prevention purposes, in accordance with applicable data protection law

Kiranlab UK does not sell, share, or transfer your data or query results to any third parties.

---

## 7. Security Responsibilities

You are responsible for:

- Ensuring the Azure account used has the minimum necessary permissions (Microsoft Sentinel Reader + Security Reader)
- Protecting your Azure credentials and API tokens
- Not using the service to access workspaces for which you do not have authorisation
- Reporting suspected security vulnerabilities via the GitHub repository

Kiranlab UK implements reasonable security controls, including TLS encryption, rate limiting, and IP-level access controls. However, no system is unconditionally secure, and Kiranlab UK cannot guarantee protection against all possible threats.

---

## 8. Acceptable Use

You agree not to use Sentinel Foundry to:

- Access workspaces or Azure resources without authorisation
- Conduct automated scraping, load testing, or denial-of-service attacks
- Circumvent rate limits or access controls
- Violate any applicable law or regulation
- Reverse engineer or attempt to extract the server-side implementation beyond what is published as open source

Abuse of the hosted service may result in permanent IP-level blocking without notice.

---

## 9. Compliance

You are responsible for ensuring your use of Sentinel Foundry complies with all applicable laws and regulations in your jurisdiction, including but not limited to:

- **UK GDPR / Data Protection Act 2018** (for users in the United Kingdom)
- **GDPR** (for users in the European Economic Area)
- **Your organisation's information security policies**
- **Microsoft's terms** governing the Azure services accessed

Sentinel Foundry is a **read-only tool** — it does not create, modify, or delete resources in your Azure environment. However, you remain responsible for the Azure resources and data you grant access to.

---

## 10. Changes to Terms

Kiranlab UK reserves the right to update these terms at any time. Continued use of the service after changes are published constitutes acceptance of the updated terms. Material changes will be noted in the repository's commit history.

---

## 11. Governing Law

These terms are governed by the laws of **United Kingdom**. Any disputes arising from these terms or your use of the service shall be subject to the exclusive jurisdiction of the relevant courts of law.

---

## 12. Contact

For legal enquiries, partnership requests, or to report policy violations, please open an issue in the GitHub repository or contact Kiranlab UK via the repository.

---

*© 2026 Kiranlab UK. All rights reserved.*
