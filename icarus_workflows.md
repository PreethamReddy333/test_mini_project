# Icarus Agentic Workflows
## Capital Market Surveillance & Compliance Dashboard

This document showcases natural language workflows that demonstrate Icarus's agentic capabilities across multiple MCPs. Each workflow shows:
- **Elaborate Version**: First-time execution with full context (for demos)
- **Context Version**: Subsequent execution leveraging cached parameters

---

## Workflow 1: Insider Trading Investigation

**Scenario**: A tip indicates that an employee may have traded on confidential UPSI before a major announcement.

### Elaborate Version (First Time)
```
1. "Show me all active UPSI for RELIANCE Industries in the last 30 days"
   → UPSI Database MCP

2. "Who accessed the Q3 earnings UPSI for RELIANCE? Show me the access log"
   → UPSI Database MCP

3. "Check if entity ENT-0001 is an insider for RELIANCE"
   → Entity Relationship MCP

4. "Did ENT-0001 make any trades on RELIANCE during the closed trading window?"
   → Trade Data MCP + UPSI Database MCP

5. "This looks suspicious. Create a Jira ticket to investigate ENT-0001 for potential insider trading on RELIANCE"
   → Jira MCP

6. "Generate an STR report for this case with entity ENT-0001 and symbol RELIANCE"
   → Regulatory Reports MCP
```

### Context Version (With Cache)
```
1. "Show active UPSI for RELIANCE"
2. "Who accessed this?"
3. "Is ENT-0001 an insider?"
4. "Did they trade during closure?"
5. "Create a Jira ticket for this"
6. "Generate STR report"
```

---

## Workflow 2: Market Manipulation Detection (Wash Trading)

**Scenario**: Unusual trading patterns detected on a mid-cap stock suggesting potential wash trading.

### Elaborate Version (First Time)
```
1. "Analyze volume patterns for TCS stock over the last week"
   → Trade Data MCP

2. "Check for wash trading between entity FUND-ABC and any related counterparties on TCS"
   → Anomaly Detection MCP

3. "Show me the relationship graph for FUND-ABC - are there any connected entities?"
   → Entity Relationship MCP

4. "Get all trades by FUND-ABC and its connected entities on TCS today"
   → Trade Data MCP

5. "This is confirmed wash trading. Send a Slack alert to the compliance team with severity HIGH"
   → Slack Notifier MCP

6. "Create a case in the dashboard for wash trading by FUND-ABC on TCS with priority CRITICAL"
   → Dashboard Webserver
```

### Context Version (With Cache)
```
1. "Analyze TCS volume"
2. "Check for wash trading on this stock"
3. "Show FUND-ABC relationships"
4. "Get their trades on TCS"
5. "Send Slack alert - HIGH severity"
6. "Create a CRITICAL case for this"
```

---

## Workflow 3: Front-Running Investigation

**Scenario**: A broker is suspected of trading ahead of large client orders.

### Elaborate Version (First Time)
```
1. "Get large orders above ₹50 lakhs value for INFY stock today"
   → Trade Data MCP

2. "Detect front-running patterns for broker BROKER-X on INFY by comparing proprietary trades before client trades"
   → Anomaly Detection MCP

3. "Show me BROKER-X's trading profile and activity summary"
   → Trade Data MCP

4. "Check if BROKER-X has any family or business connections to the client entity"
   → Entity Relationship MCP

5. "Create a Jira ticket with HIGH priority: Potential front-running by BROKER-X on INFY"
   → Jira MCP

6. "Push an alert to the dashboard with severity HIGH for front-running detection"
   → Dashboard Webserver
```

### Context Version (With Cache)
```
1. "Large orders on INFY"
2. "Detect front-running by BROKER-X"
3. "Show broker's trading profile"
4. "Any connections to clients?"
5. "Create Jira ticket - HIGH priority"
6. "Push alert to dashboard"
```

---

## Workflow 4: Trading Window Violation Check

**Scenario**: Quarterly earnings are being released and we need to verify trading window compliance.

### Elaborate Version (First Time)
```
1. "What is the current trading window status for HDFC Bank?"
   → UPSI Database MCP

2. "List all designated persons and insiders for HDFC Bank"
   → Entity Relationship MCP

3. "Did any of the HDFC Bank insiders trade during the last closure period?"
   → Trade Data MCP + UPSI Database MCP

4. "Show me the specific trades made by insider KMP-001 on HDFC Bank in December"
   → Trade Data MCP

5. "This is a window violation. Create a compliance case in the dashboard with status OPEN"
   → Dashboard Webserver

6. "Generate a compliance scorecard for entity KMP-001"
   → Regulatory Reports MCP
```

### Context Version (With Cache)
```
1. "Trading window for HDFC?"
2. "List HDFC insiders"
3. "Did insiders trade during closure?"
4. "Show KMP-001's trades in December"
5. "Create compliance case"
6. "Generate their scorecard"
```

---

## Workflow 5: Pump and Dump Detection

**Scenario**: A penny stock shows unusual price and volume spikes suggesting manipulation.

### Elaborate Version (First Time)
```
1. "Detect volume anomalies for stock PENNY-001 over the last 5 trading days"
   → Trade Data MCP

2. "Run pump and dump detection analysis on PENNY-001 with a 60-minute window"
   → Anomaly Detection MCP

3. "Who are the top 5 traders driving volume in PENNY-001?"
   → Trade Data MCP

4. "Check if any of these top traders are connected to each other"
   → Entity Relationship MCP

5. "This looks like coordinated manipulation. Send a CRITICAL Slack alert with details"
   → Slack Notifier MCP

6. "Register these entities as high-risk in the dashboard with risk score 95"
   → Dashboard Webserver
```

### Context Version (With Cache)
```
1. "Volume anomalies on PENNY-001"
2. "Pump and dump check"
3. "Top traders for this stock"
4. "Are they connected?"
5. "Send CRITICAL Slack alert"
6. "Register as high-risk entities"
```

---

## Workflow 6: End-of-Day Surveillance Summary

**Scenario**: Generate a comprehensive end-of-day report for compliance review.

### Elaborate Version (First Time)
```
1. "Show me today's dashboard stats - total alerts, open cases, and workflow count"
   → Dashboard Webserver

2. "List all CRITICAL and HIGH severity alerts from today"
   → Dashboard Webserver

3. "Generate a market surveillance report for today covering all anomalies detected"
   → Regulatory Reports MCP

4. "Show all open investigation cases with status INVESTIGATING"
   → Dashboard Webserver

5. "Send end-of-day summary to compliance Slack channel with alert counts"
   → Slack Notifier MCP
```

### Context Version (With Cache)
```
1. "Today's dashboard stats"
2. "Critical alerts today"
3. "Generate surveillance report"
4. "Open investigation cases"
5. "Send EOD summary to Slack"
```

---

## Workflow 7: Entity Risk Profiling

**Scenario**: Deep-dive risk assessment for a flagged entity before onboarding or during periodic review.

### Elaborate Version (First Time)
```
1. "Search for entity TRADER-007 and show their profile details"
   → Entity Relationship MCP

2. "Show all relationships and connections for TRADER-007 within 2 hops"
   → Entity Relationship MCP

3. "Is TRADER-007 an insider for any listed company?"
   → Entity Relationship MCP

4. "Get TRADER-007's complete trading history and account activity"
   → Trade Data MCP

5. "Run anomaly scans on all of TRADER-007's recent trades"
   → Anomaly Detection MCP

6. "Generate a full entity risk report for TRADER-007"
   → Regulatory Reports MCP
```

### Context Version (With Cache)
```
1. "Search TRADER-007"
2. "Show their connections"
3. "Are they an insider?"
4. "Trading history"
5. "Scan for anomalies"
6. "Generate risk report"
```

---

## Workflow 8: Real-Time Alert Response

**Scenario**: A high-severity alert just triggered and needs immediate investigation.

### Elaborate Version (First Time)
```
1. "Show me the latest CRITICAL alert from the dashboard"
   → Dashboard Webserver

2. "Get details of entity ENT-ALERT-001 mentioned in this alert"
   → Entity Relationship MCP

3. "Fetch all trades by ENT-ALERT-001 in the last hour"
   → Trade Data MCP

4. "Create an urgent Jira ticket: CRITICAL - Real-time manipulation alert for ENT-ALERT-001"
   → Jira MCP

5. "Send immediate Slack notification to #compliance-urgent channel"
   → Slack Notifier MCP

6. "Update the case in dashboard to status INVESTIGATING with assignment to compliance lead"
   → Dashboard Webserver
```

### Context Version (With Cache)
```
1. "Latest CRITICAL alert"
2. "Get entity details"
3. "Their trades in last hour"
4. "Create urgent Jira ticket"
5. "Slack to #compliance-urgent"
6. "Update case to INVESTIGATING"
```

---

## Summary: MCP Coverage

| MCP | Primary Use Cases |
|-----|------------------|
| **UPSI Database** | UPSI records, trading windows, access logs |
| **Trade Data** | Trade fetching, volume analysis, account profiles |
| **Entity Relationship** | Connections, insider status, relationship graphs |
| **Anomaly Detection** | Spoofing, wash trading, front-running, pump & dump |
| **Regulatory Reports** | STR, surveillance reports, compliance scorecards |
| **Jira** | Case/ticket creation and management |
| **Slack Notifier** | Real-time team notifications |
| **Dashboard** | Centralized stats, alerts, cases, workflows |

---

## Key Benefits of Context Caching

1. **Reduced Input**: After first query, subsequent queries can use shortened prompts
2. **Entity Resolution**: "this entity" / "they" / "the trader" resolves to last queried entity
3. **Symbol Resolution**: "this stock" / "the symbol" resolves to last queried symbol
4. **Case Continuity**: Investigation flows naturally without re-specifying parameters
5. **Natural Conversation**: Workflows feel like talking to a human analyst

---

*Document generated for Icarus Capital Market Surveillance Demo*
