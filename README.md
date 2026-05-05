<img src="assets/banner.svg" alt="Sentinel Foundry — AI Intelligence Layer for Microsoft Sentinel" width="100%"/>

<div align="center">

> **🔵 Public Preview** — Sentinel Foundry is live and available for public testing. We welcome your valuable feedback.

**Hosted service available: Monday – Sunday, 07:00 – 22:00 UK Time (GMT/BST) until 31-05-2026**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![MCP Protocol](https://img.shields.io/badge/Protocol-MCP-0078d4)](https://modelcontextprotocol.io)
[![Azure Sentinel](https://img.shields.io/badge/Microsoft-Sentinel-0078d4)](https://azure.microsoft.com/products/microsoft-sentinel)

</div>

---

# Sentinel Foundry — MCP Server

**Sentinel Foundry** is an open-source AI intelligence layer for Microsoft Sentinel, built on the [Model Context Protocol (MCP)](https://modelcontextprotocol.io) — the open standard for connecting AI assistants to live systems.

Connect directly from VS Code Copilot Chat or Claude Desktop and talk to your Sentinel workspace in plain English. No dashboards. No KQL required.

---

## What is this?

Most security teams spend time *finding* information: digging through dashboards, writing KQL queries, switching between portals. Sentinel Foundry eliminates that by giving your AI assistant **direct, live access** to your Microsoft Sentinel workspace.

Ask in plain English. Get real answers from your real data — instantly.

**You ask:** *"Why is our security score dropping? What should we fix first?"*
**It does:** Runs health checks, analyses detection coverage, cross-references costs, and tells you exactly what to prioritise — in seconds.

**You ask:** *"Would we detect a ransomware attack right now?"*
**It does:** Maps 77 MITRE ATT&CK v18 techniques against your enabled rules and data. Returns a pass/fail verdict for each technique with specific gaps identified.

Every answer comes from **live Azure APIs** against your actual workspace — not guesses or cached training data.

---

## Why use this?

| Without Sentinel Foundry | With Sentinel Foundry |
|---|---|
| Hours writing KQL queries | Answers in seconds, plain English |
| Switching between 5 different portals | One conversation with your AI assistant |
| Manual MITRE ATT&CK gap analysis | Automated coverage across 77 techniques |
| Guessing which tables drive your bill | Exact cost breakdown with savings recommendations |
| Writing board reports from scratch | AI-generated narrative calibrated for any audience |
| Manual detection rule tuning | Automated false-positive analysis with KQL fixes |

**Who benefits:**
- **Security Operations teams** — faster triage, investigation, and threat hunting
- **Security Managers and CISOs** — instant posture summaries and board-ready reports
- **Security Architects** — detection gap analysis and coverage recommendations
- **FinOps teams** — accurate cost visibility with regional currency pricing
- **The security community** — open-source, extensible, and free to self-host

---

## What can it do?

**43 tools** across every dimension of Sentinel operations:

| What you ask | What happens |
|---|---|
| *"What are our top cost drivers this month?"* | Reads Azure billing data, breaks down spend by table in your regional currency (USD, GBP, EUR, AUD, and more) |
| *"Do we have detection gaps against MITRE ATT&CK?"* | Maps all 14 ATT&CK v18 tactics across 77 techniques and surfaces what's uncovered |
| *"Which detection rules are causing the most noise?"* | Analyses 30 days of alert data, finds high false-positive rules, provides ready-to-deploy KQL fixes |
| *"Give me our full security health score"* | Scores Data, Detection, Automation, Cost, and Operations pillars with evidence |
| *"What workbooks are we missing?"* | Cross-references your data sources against workbook coverage |
| *"Suggest automations we should build"* | Analyses incident patterns, returns Logic App templates ready to deploy |
| *"Generate a full security posture report"* | Produces an HTML report with score rings, metric cards, and print-to-PDF support |
| *"Why does our workspace score so low?"* | Runs root-cause diagnosis across all pillars — identifies the real reasons, not just symptoms |
| *"Would we detect a ransomware attack right now?"* | Simulates a named attack scenario against your live data, returns pass/fail per MITRE technique |
| *"Write a board summary of our security posture"* | Generates a plain-English executive narrative — no technical jargon |
| *"Show me PowerShell executions in the last 24 hours"* | Queries DeviceProcessEvents via Defender XDR Advanced Hunting |
| *"Analyse and score our detection rule quality"* | Per-rule scores across 5 dimensions: KQL, severity, entity mapping, MITRE, and freshness |
| *"Our Sentinel bill jumped — what changed?"* | Identifies ingestion spikes and waste patterns with actionable savings recommendations |

---

## Connect in 2 minutes

### VS Code Copilot Chat

**Step 1** — Open VS Code and press `Ctrl+Shift+P` → search for **MCP: Add Server**

**Step 2** — Choose **HTTP** and enter:
```
https://mcp.kiranlab.co.uk/sentinel
```

**Step 3** — Add your configuration to VS Code `settings.json`:

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

**Step 4** — Open Copilot Chat (`Ctrl+Alt+I`), switch to **Agent mode**, and run:
> *"Discover my Sentinel workspaces and connect automatically."*

If one Sentinel workspace is found, it is connected automatically.
If multiple workspaces are found, you will be asked which one to use.
The selected workspace subscription and resource group are resolved automatically.

When you first run a Sentinel query, you will be prompted to sign in with your Azure account. Your credentials are used only within your session and are never stored.

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

> **That's it.** No write access is needed. The agent is read-only and cannot create, modify, or delete anything in your Azure environment.

### Microsoft Graph (Defender XDR only — optional)

| Permission | Purpose |
|---|---|
| `ThreatHunting.Read.All` | Run Advanced Hunting queries against Defender XDR tables via Graph Security API |

This is only needed if you want to query Defender XDR tables (`DeviceEvents`, `AlertInfo`, etc.) alongside your Sentinel workspace.

To get a Graph token:
```bash
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

## Tool Categories

<details>
<summary><strong>🔎 Schema &amp; Tables (5 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `list_tables` | Lists all Log Analytics tables in your workspace with row counts and last-updated timestamps — plus all 38 Defender XDR tables when the Graph token is configured |
| `get_schema` | Returns full column schema for any table |
| `get_sample_logs` | Returns recent sample rows from a table |
| `list_data_connectors` | Lists all configured data connectors with health status |
| `classify_tables` | Categorises tables by security domain (Identity, Endpoint, Network, Cloud, Application) |

</details>

<details>
<summary><strong>❤️ Health &amp; Security Posture (4 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `analyze_sentinel_health` | Full health report: connector gaps, disabled rules, stale data, misconfigurations |
| `calculate_security_score` | Weighted Secure Vision Score (0–100) across 6 pillars with per-pillar evidence |
| `run_daily_assessment` | Lightweight daily posture check — faster snapshot than full score calculation |
| `get_score_trend` | Returns score history for trend analysis |

</details>

<details>
<summary><strong>🧠 Reasoning &amp; Intelligence (5 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `diagnose_workspace` | Runs all modules in parallel, applies 10 correlation rules to identify root causes with score-impact estimates |
| `analyze_value_efficiency` | Cross-references ingestion cost against active detection rules — shows tables you pay for but don't detect against |
| `simulate_attack` | Maps 77 MITRE ATT&CK v18 techniques across 11 scenarios to your available tables and enabled rules |
| `generate_narrative` | Produces audience-calibrated narrative: board / CISO / SOC / technical |
| `get_session_context` | Returns all findings from this session so follow-up prompts are instant |

</details>

<details>
<summary><strong>🛡️ Detection &amp; MITRE ATT&amp;CK (10 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `list_detection_rules` | All analytic rules with status, MITRE mapping, and optional quality filter |
| `analyze_detection_coverage` | Full MITRE ATT&CK v18 coverage heatmap across all 14 enterprise tactics |
| `detect_gaps` | Identifies highest-priority uncovered tactics with business-impact explanation |
| `score_detection_quality` | Per-rule quality scores across 5 dimensions |
| `analyze_incidents` | Incident volume, MTTR, false-positive rate, top noisy rules, closure patterns |
| `tune_detection_rules` | 30-day alert cross-reference → specific KQL exclusion patches with real entity values |
| `suggest_detection_rules` | Generates ready-to-deploy KQL rules for uncovered MITRE techniques |
| `suggest_hunting_queries` | Returns runnable KQL hunting queries for your available tables |
| `generate_detection_rule` | AI-generates a new Sentinel analytics rule with KQL, severity, and MITRE mapping |
| `generate_kql` | Generates ad-hoc KQL for any security investigation question |

</details>

<details>
<summary><strong>💰 Cost &amp; Waste (3 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `analyze_cost` | Reads actual billed GB from Azure Usage — monthly estimate, per-table breakdown, live regional pricing in your local currency (USD, GBP, EUR, AUD, JPY, CAD, INR, and more) |
| `detect_waste` | Identifies over-ingested tables, verbose sources, and zero-value data streams |
| `suggest_cost_optimizations` | Ranked savings plan with currency-specific estimates and effort ratings |

</details>

<details>
<summary><strong>📊 Workbooks (4 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `list_workbooks` | All deployed workbooks with last-modified dates |
| `analyze_workbooks` | Coverage assessment — which domains have workbooks, which are missing |
| `suggest_workbooks` | Recommends workbooks based on your data sources and gaps |
| `generate_workbook` | Generates a complete Sentinel workbook ARM template ready to deploy |

</details>

<details>
<summary><strong>🤖 Automation &amp; Reporting (8 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `suggest_automations` | Identifies automation opportunities from incident patterns with Logic App templates |
| `suggest_improvements` | Prioritised improvement roadmap across all pillars |
| `suggest_notebooks` | Recommends Jupyter notebooks for investigation workflows |
| `generate_executive_report` | Executive HTML summary with score rings and metric cards |
| `generate_soc_report` | SOC operational report with actionable items |
| `generate_engineering_report` | Technical engineering report for the security team |
| `run_daily_assessment` | Lightweight daily posture snapshot |
| `analyze_value_efficiency` | Cost vs detection yield — which ingestion is earning its cost |

</details>

---

## How It Works

```
Your Question
     │
     ▼
VS Code Copilot / Claude Desktop
     │  (MCP protocol — encrypted HTTPS connection)
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

**Core principles:**

- **Read-only** — the server never writes to, modifies, or deletes anything in your Azure environment
- **Session-isolated** — each user connection is fully independent; your workspace credentials are never shared with other users
- **Live data only** — every answer is derived from your actual Azure APIs at query time
- **Zero data retention** — no logs, no storage of query results or workspace data on the server

---

## Service Protection

The hosted service at `mcp.kiranlab.co.uk` is enterprise-grade protected against common threats. It is designed to be always available and resilient to abuse, with automatic protection that keeps the service running reliably for legitimate users. It operates within a dedicated, isolated network environment — completely separate from any other Kiranlab infrastructure.

---

## Service Availability

> **🕘 Monday – Friday: 09:00 – 18:00 UK Time (GMT/BST)**

The hosted MCP server is available during these hours for public preview. Outside of these hours the service may be offline for maintenance.

If you need extended availability or an enterprise SLA, please reach out via GitHub issues or the contact details in [TERMS.md](TERMS.md).

**Self-hosting:** The server is fully open-source — you can run your own instance 24/7 by following the deployment guide in the repository.

---

## Example Conversations

**Security posture review:**
> *"Give me a complete security posture report for our workspace. Score each pillar and tell me what to prioritise."*

**Cost investigation:**
> *"Our Sentinel bill jumped 40% last month. Which tables are driving the increase and how do we reduce costs?"*

**Detection tuning:**
> *"We're getting too many false positives. Analyse our detection rules and give me KQL patches to fix the noisiest ones."*

**Threat coverage gap:**
> *"Are we detecting lateral movement? Show me our MITRE ATT&CK coverage and what we're missing."*

**Incident review:**
> *"Summarise our incidents from the last 7 days. What are the top alert sources and what should we automate first?"*

**Attack simulation:**
> *"Simulate a ransomware attack against our workspace. Would we detect each technique? Where are the gaps?"*

**Board report:**
> *"Write a plain-English board summary of our current security posture. No technical jargon."*

**Defender XDR hunting:**
> *"Show me PowerShell executions from DeviceProcessEvents in the last 24 hours. Are any of these processes associated with active alerts?"*

---

## Defender XDR Advanced Hunting

In addition to Sentinel Log Analytics, the agent supports **Microsoft Defender XDR** as a second data plane — enabling unified queries across both platforms in the same conversation.

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

---

## Contributing

Sentinel Foundry is open-source and community-driven. We would love your help making it better.

**Ways to contribute:**
- 🐛 **Report bugs** — open a [GitHub Issue](https://github.com/prabhukiranveesam/Sentinel-Foundry/issues)
- 💡 **Suggest features** — what tools or improvements would help your team?
- 🔧 **Submit a pull request** — new detection rules, KQL improvements, cost optimisations
- 📖 **Improve documentation** — clearer explanations, better examples
- 🌍 **Share with the community** — if this helped your team, spread the word

**Interested in contributing?** Open a GitHub Issue or Discussion and introduce yourself. All experience levels welcome — security engineers, developers, and documentation writers alike.

> *"Security is a community effort. The more people who can access and understand their Sentinel workspace, the better protected we all are."*

---

## About

Sentinel Foundry is built on the [Model Context Protocol](https://modelcontextprotocol.io) — the open standard for connecting AI assistants to live data sources.

**43 tools. 11 guided prompts. Full MITRE ATT&CK v18 coverage across all 14 enterprise tactics.**

The reasoning engine runs all analytical modules in parallel, applies 10 correlation rules, and tells you *why* your workspace is in its current state — not just what the numbers are.

The source code for this MCP server is available under the [MIT License](LICENSE).

> For access, enterprise deployment enquiries, or to report issues, open a [GitHub Issue](https://github.com/prabhukiranveesam/Sentinel-Foundry/issues) or contact via the repository.

---

*Sentinel Foundry is an independent open-source project. It is not affiliated with, endorsed by, or a product of Microsoft Corporation. Microsoft Sentinel, Azure, and related trademarks are the property of Microsoft Corporation. See [TERMS.md](TERMS.md) for full legal terms.*

*© 2026 Kiranlab UK. All rights reserved. Code released under the MIT License.*
