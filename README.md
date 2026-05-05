<img src="assets/banner.svg" alt="Sentinel Foundry — AI Intelligence Layer for Microsoft Sentinel" width="100%"/>

# Sentinel Foundry — MCP Server

**Sentinel Foundry** is an open-source AI intelligence layer for Microsoft Sentinel, built on the [Model Context Protocol (MCP)](https://modelcontextprotocol.io) — the open standard for connecting AI assistants to live systems.

Connect directly from VS Code Copilot Chat or Claude Desktop and talk to your Sentinel workspace in plain English. No dashboards. No KQL required.

---

## What is this?

Most security teams spend time *finding* information: digging through dashboards, writing KQL, switching between portals. Sentinel Foundry eliminates that by giving your AI assistant **direct, live access** to your Sentinel workspace data.

Ask in plain English. Get real answers from your real data.

**You ask:** *"Why is our security score dropping? What should we fix first?"*
**It does:** Runs health checks, analyses detection coverage, cross-references costs, applies a reasoning engine across all findings, and tells you exactly what to prioritise — in seconds.

**You ask:** *"Would we detect a ransomware attack right now?"*
**It does:** Maps 77 MITRE ATT&CK v18 techniques against your enabled rules and available data tables. Returns a pass/fail verdict for each technique with specific gaps.

This is not a chatbot guessing from training data. Every answer comes from **live Azure APIs** against your actual workspace.

---

## What can it do?

**43 tools** across every dimension of Sentinel operations — from cost analysis to threat simulation:

| What you ask | What happens |
|---|---|
| *"What are our top cost drivers this month?"* | Reads Azure billing data, breaks down ingestion GB and spend by table, in your regional currency |
| *"Do we have any detection gaps against MITRE ATT&CK?"* | Maps all 14 ATT&CK v18 tactics across 77 techniques, surfaces uncovered areas |
| *"Which detection rules are causing the most noise?"* | Analyses 30 days of alert data, finds high-FP rules, provides KQL patches |
| *"Give me our full security health score"* | Scores Data, Detection, Automation, Cost, and Operations pillars with evidence |
| *"What workbooks are we missing?"* | Cross-references your data sources against workbook coverage |
| *"Suggest automations we should build"* | Analyses incident patterns, returns Logic App ARM templates ready to deploy |
| *"Generate a full security posture report"* | Produces a self-contained HTML report with score rings, metric cards, and print-to-PDF support |
| *"Why does our workspace score so low?"* | Runs root-cause diagnosis across all pillars — 10 correlation rules identify the real reasons |
| *"Would we detect a ransomware attack right now?"* | Simulates a named attack scenario against live data, returns pass/fail per MITRE technique |
| *"Write a board summary of our current security posture"* | Generates an audience-calibrated narrative: board / CISO / SOC / technical |
| *"Show me PowerShell executions in the last 24 hours"* | Queries DeviceProcessEvents via Defender XDR Advanced Hunting |
| *"Analyse our detection rules and score their quality"* | Per-rule quality scores across 5 dimensions: KQL, severity, entity mapping, MITRE, and freshness |
| *"Our Sentinel bill jumped — what changed?"* | Identifies ingestion spikes, over-ingested tables, and waste patterns with actionable savings recommendations |

---

## Tool Categories

<details>
<summary><strong>🔎 Schema & Tables (5 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `list_tables` | Lists all Log Analytics tables in your workspace with row counts and last-updated timestamps — plus all 38 Defender XDR tables when `X-Security-Token` is configured |
| `get_schema` | Returns full column schema for any table (Log Analytics or Defender XDR) |
| `get_sample_logs` | Returns recent sample rows from a table — progressive fallback P1D→P7D→P30D→P90D for LA tables; 7-day Timestamp filter via Graph API for Defender XDR tables |
| `list_data_connectors` | Lists all configured data connectors with health status |
| `classify_tables` | Categorises tables by security domain (Identity, Endpoint, Network, Cloud, Application) |

</details>

<details>
<summary><strong>❤️ Health & Security Posture (4 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `analyze_sentinel_health` | Full health report: connector gaps, disabled rules, stale data, misconfigurations |
| `calculate_security_score` | Weighted Secure Vision Score (0–100) across 6 pillars with per-pillar evidence |
| `run_daily_assessment` | Lightweight daily posture check — faster snapshot than full score calculation |
| `get_score_trend` | Returns score history for trend analysis over N days |

</details>

<details>
<summary><strong>🧠 Reasoning & Intelligence (5 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `diagnose_workspace` | **Primary reasoning tool** — runs all modules in parallel, applies 10 correlation rules to identify root causes with score-impact estimates |
| `analyze_value_efficiency` | Cross-references ingestion cost against active detection rules — exposes tables paid for but not detected against |
| `simulate_attack` | Maps 77 MITRE ATT&CK v18 techniques across 11 scenarios to available tables and enabled rules — returns a readiness verdict |
| `generate_narrative` | Produces audience-calibrated narrative from session findings: board / CISO / SOC / technical |
| `get_session_context` | Returns all findings cached this session so subsequent prompts avoid re-querying Azure |

</details>

<details>
<summary><strong>🛡️ Detection & MITRE ATT&CK (10 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `list_detection_rules` | All analytic rules with status, MITRE mapping, and optional quality filter |
| `analyze_detection_coverage` | Full MITRE ATT&CK v18 coverage heatmap across all 14 enterprise tactics |
| `detect_gaps` | Identifies highest-priority uncovered tactics with business-impact explanation |
| `score_detection_quality` | Per-rule quality scores across 5 dimensions (KQL, severity, entity mapping, MITRE, freshness) |
| `analyze_incidents` | Incident volume, MTTR, false-positive rate, top noisy rules, closure patterns |
| `tune_detection_rules` | 30-day alert + FP cross-reference → specific KQL exclusion patches with real entity values |
| `suggest_detection_rules` | Generates ready-to-deploy KQL rules for the top uncovered MITRE techniques |
| `suggest_hunting_queries` | Returns runnable KQL hunting queries for tables available in your workspace |
| `generate_detection_rule` | AI-generates a new Sentinel analytics rule (name, KQL, severity, MITRE mapping) |
| `generate_kql` | Generates ad-hoc KQL for any security investigation question |

</details>

<details>
<summary><strong>💰 Cost & Waste (3 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `analyze_cost` | Reads actual billed GB from Azure Usage — monthly estimate, per-table breakdown, regional pricing in your local currency (GBP, USD, EUR, AUD, JPY, CAD, INR, and more) |
| `detect_waste` | Identifies over-ingested tables, verbose sources, and zero-value data streams |
| `suggest_cost_optimizations` | Ranked savings plan with currency-specific estimates and effort ratings |

</details>

<details>
<summary><strong>📊 Workbooks (4 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `list_workbooks` | All deployed Sentinel workbooks with metadata |
| `analyze_workbooks` | Coverage gaps and stale workbook review |
| `suggest_workbooks` | Recommended workbooks to build based on available data sources |
| `generate_workbook` | Generates a Sentinel workbook ARM template for a given use case |

</details>

<details>
<summary><strong>🤖 Automation & Response (4 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `suggest_automations` | Reads incident history, scores scenarios, returns top 3 with ready-to-deploy Logic App ARM templates |
| `suggest_notebooks` | Checks available tables and returns which Jupyter notebook scenarios are ready to run |
| `generate_playbook` | Generates a Logic App playbook ARM template for a named incident response scenario |
| `generate_notebook` | Generates a Jupyter notebook for a named investigation workflow |

</details>

<details>
<summary><strong>📋 Reporting (3 tools)</strong></summary>

All reports default to **self-contained HTML** — professional design with score rings, metric cards, and print-friendly CSS. After every report the agent offers PDF export instructions (File → Print → Save as PDF).

| Tool | What it does |
|---|---|
| `generate_executive_report` | Full executive report — score, findings, risk assessment, recommendations |
| `generate_soc_report` | SOC operations report — incident analysis, alert fatigue, tuning recommendations |
| `generate_engineering_report` | Engineering deep-dive — detection coverage, rule quality, KQL improvements |

</details>

<details>
<summary><strong>⚙️ Improvements (2 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `suggest_improvements` | General improvement recommendations across all pillars, prioritised by impact and effort |
| `assess_table` | Deep assessment of a single table — coverage, quality, cost contribution |

</details>

<details>
<summary><strong>📡 Monitoring (2 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `run_daily_assessment` | Lightweight daily posture check with trend comparison |
| `get_score_trend` | Score history and trend analysis over a configurable number of days |

</details>

<details>
<summary><strong>🔧 Workspace Management (3 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `discover_workspaces` | Auto-detects all Sentinel workspaces the signed-in user has access to |
| `set_workspace` | Manually connect to a specific workspace by subscriptionId, resourceGroup, name |
| `get_workspace` | Shows which workspace is currently active |

</details>

---

## Connect in 2 minutes

To add the Sentinel Foundry collection, first set up the MCP server interface. Follow the step-by-step instructions for the compatible AI-powered code editors and agent-building platforms.
The Sentinel Foundry collection is hosted at the following URL:
```json

https://mcp.kiranlab.co.uk/sentinel

```

### VS Code Copilot (recommended)
To add Sentinel Foundry custom tools in Visual Studio Code, follow these steps:

1. Add MCP server:


  a. Press Ctrl + Shift + P then type or choose MCP: Add Server.

   <img width="602" height="112" alt="mcp-get-started-add-server" src="https://github.com/user-attachments/assets/541c3249-8224-4e89-9f6f-86b49e97e433" />
   
   b. Choose HTTP (HTTP or Server-Sent Events).

   <img width="599" height="204" alt="mcp-get-started-http" src="https://github.com/user-attachments/assets/d2af653f-0e8d-4def-8aa1-cc31b7a0b839" />
   
   c. Enter the URL as `https://mcp.kiranlab.co.uk/sentinel` to add our custom tools, then press Enter.

   d. Assign a friendly Server ID (for example, Sentinel Foundry - MCP server)
   
   e. Choose whether to make the server available in all Visual Studio Code workspaces or just the current one.
   
3. Allow authentication. When prompted, select Allow to authenticate with an account that has **Microsoft Sentinel Reader** and **Security Reader** roles.

   <img width="615" height="138" alt="mcp-get-started-authenticate" src="https://github.com/user-attachments/assets/3b54d1ac-b70e-499a-810b-8f4e8103078e" />
   
4. Open Visual Studio Code's chat. Select View > Chat, select the Toggle Chat icon  beside the search bar, or press Ctrl + Alt + I.

5. Verify connection. Set the chat to Agent mode, then confirm by selecting the Configure Tools icon that you see added under the MCP server.

   <img width="687" height="282" alt="mcp-get-started-04" src="https://github.com/user-attachments/assets/919c267b-bb62-46a3-9cc3-174d2073768d" />
   
6. The agent auto-detects your Sentinel workspace from your signed-in Azure account
7. Start asking questions

   (or alternatively)
   
1. Open **Settings** (`Ctrl+,`) → search **MCP**
2. Click **Edit in settings.json** and add:

```json
{
  "mcp": {
    "servers": {
      "sentinel": {
        "name": "Sentinel Foundry - MCP Server",
        "url": "https://mcp.kiranlab.co.uk/sentinel",
        "type": "http"
      }
    }
  }
}
```
3. Open **Copilot Chat** → switch to **Agent mode** (the `@` icon)
4. The agent auto-detects your Sentinel workspace from your signed-in Azure account
5. Start asking questions

> **Authentication:** The agent uses your existing VS Code Azure sign-in. No extra configuration needed — your Azure RBAC controls what you can access.

**Optional — Defender XDR Advanced Hunting:**

To also query Defender XDR tables (`DeviceEvents`, `AlertInfo`, `IdentityLogonEvents`, `EmailEvents`, etc.), add your Microsoft Graph token:

```bash
# Get a Graph token with ThreatHunting.Read.All
az account get-access-token --resource https://graph.microsoft.com --query accessToken -o tsv
```

Add the `headers` key to your MCP server entry in `settings.json`:

```json
{
  "mcp": {
    "servers": {
      "sentinel": {
        "name": "Sentinel Foundry - MCP Server",
        "url": "https://mcp.kiranlab.co.uk/sentinel",
        "type": "http",
        "headers": {
          "X-Security-Token": "<graph-token-here>"
        }
      }
    }
  }
}
```

---

### Claude Desktop

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "Sentinel Foundry - MCP Server": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://mcp.kiranlab.co.uk/sentinel",
        "--header",
        "Authorization: Bearer YOUR_API_KEY"
      ]
    }
  }
}
```

Replace `YOUR_API_KEY` with the key provided to you.

---

## Required Azure Permissions

Two Azure built-in roles cover everything the agent needs:

| Role | Scope | Covers |
|---|---|---|
| **Microsoft Sentinel Reader** | Resource group containing the workspace | Analytic rules, incidents, connectors, workbooks, watchlists, workspace query access |
| **Security Reader** | Subscription or resource group | Log Analytics table queries, workspace discovery, resource metadata |

> **That's it.** No additional roles are needed. Log Analytics Reader, Log Analytics Contributor, and Reader are all implicitly covered by this combination.
>
> **Security Reader** includes `Microsoft.OperationalInsights/workspaces/*/read` (covering all KQL queries and table enumeration) and `Microsoft.Resources/subscriptions/resourceGroups/read` (covering workspace auto-discovery).  
> **Microsoft Sentinel Reader** covers all Sentinel API operations — rules, incidents, connectors, workbooks, and billing usage data.

### Microsoft Graph (Defender XDR only, optional)

| Permission | Purpose |
|---|---|
| `ThreatHunting.Read.All` | Run Advanced Hunting queries against Defender XDR tables via Graph Security API |

This is only needed if you want to query Defender XDR tables (`DeviceEvents`, `AlertInfo`, etc.) alongside your Sentinel workspace. See the Defender XDR section for setup instructions.

---

## How It Works

```
Your Question
     │
     ▼
VS Code Copilot / Claude Desktop
     │  (MCP protocol over HTTPS — TLS 1.2/1.3)
     ▼
Sentinel Foundry MCP Server
     │  (authenticates with your Azure identity — read-only)
     │
     ├── Analytical Modules ──────────────────────────────────┐
     │   ├──► Microsoft Sentinel API  (rules, incidents)      │
     │   ├──► Log Analytics API       (KQL, schema, billing)  │
     │   └──► Azure Resource Manager  (config, workbooks)     │
     │                                                        │
     └── Reasoning Layer ◄────────────────────────────────────┘
         ├── Root Cause Engine  (10 correlation rules)
         ├── Attack Simulation  (77 MITRE v18 techniques)
         ├── Value Efficiency   (cost vs detection yield)
         └── Narrative Engine   (board/CISO/SOC/technical)
     │
     ▼
Structured response → HTML report / narrative / tool output
```

**Key design principles:**

- **Read-only** — the server never writes to, modifies, or deletes anything in your Azure environment
- **Session-isolated** — each user connection is fully independent; your workspace credentials are never shared
- **Live data only** — every answer is derived from your actual Azure APIs at query time, not cached training data
- **Zero data retention** — no logs, no storage of query results or workspace data on the server

---

## Example Conversations

**Security posture review:**
> *"Give me a complete security posture report for our workspace. Score each pillar and tell me what to prioritise."*

**Cost investigation:**
> *"Our Sentinel bill jumped 40% last month. Which tables are driving the increase and how do we reduce costs?"*

**Detection tuning:**
> *"We're getting too many false positives. Analyse our detection rules and give me KQL patches to fix the noisiest ones."*

**Threat coverage gap:**
> *"Are we detecting lateral movement? Show me our MITRE ATT&CK coverage for the Lateral Movement tactic and what we're missing."*

**Incident deep-dive:**
> *"Summarise our incidents from the last 7 days. What are the top alert sources and what should we automate first?"*

**Compliance check:**
> *"How do we align with NIST CSF? Where are the biggest gaps?"*

**Defender XDR threat hunting:**
> *"Show me PowerShell executions from DeviceProcessEvents in the last 24 hours. Are any of these processes associated with active alerts?"*

**Root-cause diagnosis:**
> *"Why does our Secure Vision Score keep dropping? Walk me through the root causes and prioritise what to fix first."*

**Attack simulation:**
> *"Simulate a ransomware attack against our workspace. Would we detect each technique? Where are the gaps?"*

**HTML report:**
> *"Generate a full engineering report for our security team as an HTML file they can open in a browser and print."*

**Narrative for the board:**
> *"Write a plain-English board summary of our current security posture. No technical jargon."*

---

## Defender XDR Advanced Hunting

In addition to classic Sentinel Log Analytics, the agent supports **Microsoft Defender XDR** as a second data plane — enabling unified queries across both platforms in the same conversation.

### Supported Tables (38)

| Domain | Tables |
|---|---|
| **Device** | `DeviceEvents`, `DeviceProcessEvents`, `DeviceNetworkEvents`, `DeviceFileEvents`, `DeviceRegistryEvents`, `DeviceLogonEvents`, `DeviceImageLoadEvents`, `DeviceInfo`, `DeviceNetworkInfo` |
| **Alerts & Incidents** | `AlertEvidence`, `AlertInfo` |
| **Email** | `EmailEvents`, `EmailAttachmentInfo`, `EmailUrlInfo`, `EmailPostDeliveryEvents` |
| **Identity** | `IdentityLogonEvents`, `IdentityQueryEvents`, `IdentityInfo`, `IdentityDirectoryEvents` |
| **Cloud Apps** | `CloudAppEvents`, `AppFileEvents` |
| **Exposure** | `ExposureGraphNodes`, `ExposureGraphEdges` |
| **Behaviour & AAD** | `BehaviorEntities`, `BehaviorInfo`, `AADSignInEventsBeta`, `AADSpnSignInEventsBeta` |
| **URL & Files** | `UrlClickEvents`, `FileProfile` |
| **Vulnerability** | `DeviceTvmSecureConfigurationAssessment`, `DeviceTvmSecureConfigurationAssessmentKB`, `DeviceTvmSoftwareInventory`, `DeviceTvmSoftwareVulnerabilities`, `DeviceTvmSoftwareVulnerabilitiesKB` |
| **Other** | `AssignedIPAddresses`, `DeviceFileCertificateInfo` |

Tool routing is **automatic** — when a KQL query or schema request targets a Defender XDR table name, it is routed to `POST https://graph.microsoft.com/v1.0/security/runHuntingQuery`. No tool changes or configuration needed beyond supplying the `X-Security-Token` header.

---

## Security

The hosted MCP server at `mcp.kiranlab.co.uk` is hardened for public access:

- **TLS 1.2/1.3 only** with HSTS (`max-age=63072000; includeSubDomains; preload`)
- **Security headers**: `X-Frame-Options: DENY`, `X-Content-Type-Options: nosniff`, `Content-Security-Policy`, `Referrer-Policy`
- **Rate limiting** on all endpoints with automatic IP-level throttling
- **Fail2ban** active — repeated authentication failures result in automatic IP bans
- **Read-only Azure access** — the server cannot create, modify, or delete Azure resources
- **No credential storage** — your Azure tokens are used only within your session and never persisted to disk

---

## About

Sentinel Foundry is built on the [Model Context Protocol](https://modelcontextprotocol.io) — the open standard for connecting AI assistants to live data sources. It runs as a session-isolated HTTPS service with full Azure identity integration.

**43 tools. 11 guided prompts. Full MITRE ATT&CK v18 coverage across all 14 enterprise tactics.**

The reasoning engine runs all analytical modules in parallel, applies 10 correlation rules, and tells you *why* your workspace is in its current state — not just what the numbers are.

Each connection is fully isolated — your session credentials and workspace data are never shared across users or retained after your session ends.

The source code for this MCP server is available in this repository under the [MIT License](LICENSE).

> For access, enterprise deployment enquiries, or to report issues, open a GitHub issue or contact via the repository.

---

*Sentinel Foundry is an independent open-source project. It is not affiliated with, endorsed by, or a product of Microsoft Corporation. Microsoft Sentinel, Azure, and related trademarks are the property of Microsoft Corporation. See [TERMS.md](TERMS.md) for full legal terms.*
