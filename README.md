<img src="assets/banner.svg" alt="Sentinel Foundry — AI-Powered Microsoft Sentinel Intelligence" width="100%"/>

# Sentinel Foundry — MCP Agent

**Sentinel Foundry** is an AI intelligence layer for Microsoft Sentinel, delivered as a live [Model Context Protocol (MCP)](https://modelcontextprotocol.io) server.

Connect directly from VS Code Copilot Chat or Claude Desktop and talk to your Sentinel workspace in plain English — no dashboards, no KQL required.

---

## What can it do?

The agent exposes **38 tools** across every dimension of Sentinel operations. Ask questions like a conversation:

| What you say | What the agent does |
|---|---|
| *"What are our top cost drivers this month?"* | Reads Azure billing data, breaks down ingestion GB and spend by table |
| *"Do we have any detection gaps against MITRE ATT&CK?"* | Maps active rules to the ATT&CK framework, surfaces uncovered techniques |
| *"Which detection rules are causing the most noise?"* | Analyses 30 days of alert data, finds high-FP rules, provides KQL patches |
| *"Give me our full security health score"* | Scores Data, Detection, Automation, Cost, and Operations pillars |
| *"What workbooks are we missing?"* | Cross-references your data sources against workbook coverage |
| *"Suggest automations we should build"* | Analyses incident patterns, returns Logic App ARM templates ready to deploy |
| *"Generate a full security posture report"* | Produces a complete PDF-ready report covering all pillars |

---

## Tool Categories

<details>
<summary><strong>🔎 Schema & Tables (5 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `list_tables` | Lists all Log Analytics tables in your workspace |
| `get_schema` | Returns full column schema for any table |
| `sample_table` | Shows recent sample rows from a table |
| `classify_tables` | Categorises tables by security domain |
| `get_table_freshness` | Checks when each data source last ingested |

</details>

<details>
<summary><strong>❤️ Health & Security Posture (4 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `analyze_sentinel_health` | Full health report: connectors, ingestion, rule status |
| `calculate_security_score` | Weighted score across 5 pillars with evidence |
| `check_data_connectors` | Connector status and freshness |
| `get_ingestion_anomalies` | Detects unusual spikes or drops in table ingestion |

</details>

<details>
<summary><strong>🛡️ Detection & MITRE ATT&CK (6 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `list_detection_rules` | All analytic rules with status and MITRE mapping |
| `analyze_detection_coverage` | MITRE ATT&CK coverage heat map |
| `detect_gaps` | Gaps vs industry baseline per tactic |
| `score_detection_quality` | Per-rule quality scores (KQL, severity, entity mapping) |
| `analyze_incidents` | Incident trends, MTTR, top alert sources + tuning signals |
| `tune_detection_rules` | 30-day noise + false-positive analysis with KQL patches |

</details>

<details>
<summary><strong>💰 Cost & Waste (3 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `analyze_cost` | Ingestion cost breakdown by table (actual Azure billing data) |
| `detect_waste` | Noisy, low-value, and duplicate tables |
| `suggest_cost_optimizations` | Actionable savings with estimated monthly reduction |

</details>

<details>
<summary><strong>📊 Workbooks (3 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `list_workbooks` | All deployed Sentinel workbooks |
| `analyze_workbooks` | Coverage gaps and stale workbooks |
| `suggest_workbooks` | Recommended workbooks to build based on your data sources |

</details>

<details>
<summary><strong>🤖 Recommendations (10 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `suggest_detection_rules` | New rules tailored to your available tables + MITRE gaps |
| `suggest_hunting_queries` | Ready-to-run KQL hunting queries for your data |
| `suggest_automations` | Logic App ARM templates for your top incident scenarios |
| `suggest_notebooks` | Jupyter notebook scenarios ready for your data sources |
| `suggest_data_connectors` | Connectors you should enable based on your environment |
| `suggest_retention_policies` | Table-by-table retention optimisation |
| `assess_table` | Deep assessment of a specific table's health and value |
| `get_recommendations` | Prioritised improvement recommendations across all pillars |
| `get_quick_wins` | High-impact, low-effort improvements to action today |
| `assess_compliance_posture` | Regulatory alignment check (NIST, ISO 27001, CIS) |

</details>

<details>
<summary><strong>📋 Reporting (3 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `generate_posture_report` | Full security posture report across all pillars |
| `generate_executive_summary` | Board-level summary with risk rating and key findings |
| `generate_compliance_report` | Compliance-focused report mapped to a chosen framework |

</details>

<details>
<summary><strong>📡 Monitoring (2 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `get_monitoring_dashboard` | Live SOC dashboard: incidents, connectors, health |
| `get_alert_trends` | Alert volume trends and anomaly detection |

</details>

<details>
<summary><strong>🔧 Workspace Management (3 tools)</strong></summary>

| Tool | What it does |
|---|---|
| `discover_workspaces` | Auto-detects all Sentinel workspaces the signed-in user has access to |
| `set_workspace` | Manually connect to a specific workspace by name |
| `get_workspace` | Shows which workspace is currently active |

</details>

---

## Connect in 2 minutes

### VS Code Copilot (recommended)

1. Open **Settings** (`Ctrl+,`) → search **MCP**
2. Click **Edit in settings.json** and add:

```json
{
  "github.copilot.chat.mcp.servers": [
    {
      "name": "Sentinel Foundry",
      "url": "https://mcp.kiranlab.co.uk/sentinel",
      "type": "http"
    }
  ]
}
```

3. Open **Copilot Chat** → switch to **Agent mode** (the `@` icon)
4. Type: `discover_workspaces` — the agent auto-detects your Sentinel workspace from your signed-in Azure account
5. Start asking questions

> **Authentication:** The agent uses your existing VS Code Azure sign-in. No extra configuration needed — your Azure RBAC controls what you can access.

---

### Claude Desktop

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "sentinel-foundry": {
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

| Role | Purpose |
|---|---|
| **Microsoft Sentinel Reader** | Read incidents, rules, and workspace data (minimum) |
| **Log Analytics Reader** | Query Log Analytics tables |
| **Reader** | Read subscription and resource metadata |
| **Log Analytics Contributor** *(optional)* | Required for billing plan lookup in cost analysis |

---

## How It Works

```
Your Question
     │
     ▼
VS Code Copilot / Claude Desktop
     │  (MCP protocol over HTTPS)
     ▼
Sentinel Foundry MCP Server
     │  (authenticates with your Azure identity)
     ├──► Microsoft Sentinel API  (rules, incidents, connectors)
     ├──► Log Analytics API       (KQL queries, schema, ingestion data)
     └──► Azure Resource Manager  (workspace config, billing, workbooks)
     │
     ▼
Structured response → AI formats → Natural language answer
```

Every answer comes from **live Azure APIs** — not training data, not estimates. The agent reads your actual workspace state.

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

---

## About

Sentinel Foundry is built on the [Model Context Protocol](https://modelcontextprotocol.io) — the open standard for connecting AI assistants to live data sources. It runs as a hardened, session-isolated HTTPS service with full Azure identity integration.

Each connection is fully isolated — your session credentials and workspace data are never shared across users.

---

*For access or enterprise deployment enquiries, contact the team via the repository.*
