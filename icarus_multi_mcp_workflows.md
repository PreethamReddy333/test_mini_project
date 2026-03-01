# Icarus Multi-MCP Agentic Workflows

> 📍 **20 Unique Surveillance Workflows** demonstrating multi-MCP orchestration in Icarus  
> Each workflow is 4-6 steps with **Natural Language prompts** + **CLI Execute commands** for cache population

---

## Contract IDs Reference

| MCP | Contract ID |
|-----|-------------|
| **anomaly_detection** | `aaaaaa4s4a4xuzmfsxs5gbs3hcm7npikux3jah52oq6rvnty63jw7qpoam` |
| **trade_data** | `aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm` |
| **upsi_database** | `aaaaaa3su7z5oaqrgs7757xyzpzp4kxi4v2uyihzf6jpjtlu7kve7ifxfi` |
| **entity_relationship** | `aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u` |
| **jira_mcp** | `aaaaaaz5hqfunhcpxhwzf5nplsgtxaydfgupn5u2at47tkz2igw7ipaya4` |
| **slack_notifier** | `aaaaaa4l5izydl4rfdxv5vmxrbdtkqka5htfq55d2d6pchqcplqv5gjbma` |
| **regulatory_reports** | `aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm` |

---

## Workflow 1: Insider Trading Investigation

**Scenario**: Detect UPSI access before suspicious trading

### Natural Language Flow
1. "Show active UPSI for RELIANCE"
2. "Who accessed this UPSI?"
3. "Get trades for ENT-0001 on RELIANCE"
4. "Did ENT-0001 trade during the closed window?"
5. "Create a Jira ticket for this investigation"

### Execute Commands
```bash
# Step 1: Get active UPSI
execute -n aaaaaa3su7z5oaqrgs7757xyzpzp4kxi4v2uyihzf6jpjtlu7kve7ifxfi -m get_active_upsi -i '{"company_symbol":"RELIANCE"}'

# Step 2: Get UPSI accessors
execute -n aaaaaa3su7z5oaqrgs7757xyzpzp4kxi4v2uyihzf6jpjtlu7kve7ifxfi -m get_upsi_accessors -i '{"upsi_id":"UPSI-FIN-001"}'

# Step 3: Get trades
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m get_trades_by_symbol -i '{"symbol":"RELIANCE","limit":50}'

# Step 4: Check window violation
execute -n aaaaaa3su7z5oaqrgs7757xyzpzp4kxi4v2uyihzf6jpjtlu7kve7ifxfi -m check_window_violation -i '{"entity_id":"ENT-0001","company_symbol":"RELIANCE","trade_timestamp":1737225600000}'

# Step 5: Create Jira ticket
execute -n aaaaaaz5hqfunhcpxhwzf5nplsgtxaydfgupn5u2at47tkz2igw7ipaya4 -m create_case_ticket -i '{"case_id":"CASE-001","subject_entity":"ENT-0001","case_summary":"Potential insider trading on RELIANCE - UPSI access before trade","priority":"High"}'
```

---

## Workflow 2: Market Manipulation Detection (Spoofing)

**Scenario**: Identify spoofing patterns and escalate

### Natural Language Flow
1. "Analyze trades for INFY today"
2. "Check for spoofing on order ORD-5001"
3. "Who is ENT-0002?"
4. "Get their relationships"
5. "Send a Slack alert about this"
6. "Generate an STR report"

### Execute Commands
```bash
# Step 1: Analyze trades
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m analyze_volume -i '{"symbol":"INFY"}'

# Step 2: Detect spoofing
execute -n aaaaaa4s4a4xuzmfsxs5gbs3hcm7npikux3jah52oq6rvnty63jw7qpoam -m detect_spoofing -i '{"order_id":"ORD-5001","entity_id":"ENT-0002","symbol":"INFY","order_details":"Large order cancelled rapidly"}'

# Step 3: Get entity details
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m get_entity -i '{"entity_id":"ENT-0002"}'

# Step 4: Get relationships
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m get_relationships -i '{"entity_id":"ENT-0002"}'

# Step 5: Send Slack alert
execute -n aaaaaa4l5izydl4rfdxv5vmxrbdtkqka5htfq55d2d6pchqcplqv5gjbma -m send_alert -i '{"alert_type":"SPOOFING","severity":"HIGH","symbol":"INFY","entity_id":"ENT-0002","description":"Spoofing detected - large order cancellation pattern","risk_score":85}'

# Step 6: Generate STR
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m generate_str -i '{"case_id":"CASE-002","entity_id":"ENT-0002","suspicious_activity_type":"SPOOFING","suspicion_reason":"Large order cancellation pattern detected"}'
```

---

## Workflow 3: Wash Trading Detection

**Scenario**: Self-dealing pattern between related accounts

### Natural Language Flow
1. "Get top traders for TCS"
2. "Check wash trading between ENT-0003 and ENT-0003"
3. "Are these entities connected?"
4. "Create a compliance ticket"
5. "Notify the team on Slack"

### Execute Commands
```bash
# Step 1: Get top traders
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m get_top_traders -i '{"symbol":"INFY","limit":10}'

# Step 2: Detect wash trading
execute -n aaaaaa4s4a4xuzmfsxs5gbs3hcm7npikux3jah52oq6rvnty63jw7qpoam -m detect_wash_trading -i '{"entity_id":"ENT-0003","counterparty_id":"ENT-0003","symbol":"INFY","trade_timestamp":1737225600000}'

# Step 3: Check entity connection
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m are_entities_connected -i '{"entity_id_1":"ENT-0003","entity_id_2":"ENT-0004","max_hops":3}'

# Step 4: Create ticket
execute -n aaaaaaz5hqfunhcpxhwzf5nplsgtxaydfgupn5u2at47tkz2igw7ipaya4 -m create_ticket -i '{"summary":"Wash Trading Alert - TCS - ENT-0003","description":"Self-dealing pattern detected between related accounts","priority":"High"}'

# Step 5: Slack notification
execute -n aaaaaa4l5izydl4rfdxv5vmxrbdtkqka5htfq55d2d6pchqcplqv5gjbma -m send_alert -i '{"alert_type":"WASH_TRADE","severity":"CRITICAL","symbol":"TCS","entity_id":"ENT-0003","description":"Wash trading detected - self-dealing pattern","risk_score":92}'
```

---

## Workflow 4: Front-Running Investigation

**Scenario**: Broker trading ahead of client orders

### Natural Language Flow
1. "Check front-running for BROKER-X on HDFC"
2. "Get trades by BROKER-X"
3. "What's BROKER-X's entity profile?"
4. "Get their connected entities"
5. "Generate investigation report"

### Execute Commands
```bash
# Step 1: Detect front-running
execute -n aaaaaa4s4a4xuzmfsxs5gbs3hcm7npikux3jah52oq6rvnty63jw7qpoam -m detect_front_running -i '{"entity_id":"BROKER-X","symbol":"HDFC","client_trade_timestamp":1737225600000,"prop_trade_timestamp":1737225595000}'

# Step 2: Get trades
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m get_trades_by_account -i '{"account_id":"BROKER-X","limit":50}'

# Step 3: Get entity
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m get_entity -i '{"entity_id":"BROKER-X"}'

# Step 4: Get connected entities
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m get_connected_entities -i '{"entity_id":"BROKER-X","max_hops":2}'

# Step 5: Generate report
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m generate_investigation_report -i '{"case_id":"CASE-003","include_evidence":true}'
```

---

## Workflow 5: Pump and Dump Detection

**Scenario**: Coordinated price manipulation

### Natural Language Flow
1. "Check pump and dump for ICICI in last hour"
2. "Analyze volume anomaly"
3. "Who are the top traders?"
4. "Get family members of top trader"
5. "Create urgent Jira ticket"
6. "Send Slack alert"

### Execute Commands
```bash
# Step 1: Detect pump and dump
execute -n aaaaaa4s4a4xuzmfsxs5gbs3hcm7npikux3jah52oq6rvnty63jw7qpoam -m detect_pump_dump -i '{"symbol":"ICICI","time_window_minutes":60}'

# Step 2: Check RSI levels
execute -n aaaaaa4s4a4xuzmfsxs5gbs3hcm7npikux3jah52oq6rvnty63jw7qpoam -m check_rsi_levels -i '{"symbol":"ICICI"}'

# Step 3: Get top traders
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m get_top_traders -i '{"symbol":"ICICI","limit":5}'

# Step 4: Get family members
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m get_family_members -i '{"entity_id":"ENT-0005"}'

# Step 5: Create ticket
execute -n aaaaaaz5hqfunhcpxhwzf5nplsgtxaydfgupn5u2at47tkz2igw7ipaya4 -m create_case_ticket -i '{"case_id":"CASE-004","subject_entity":"ENT-0005","case_summary":"Pump and dump suspected on ICICI","priority":"High"}'

# Step 6: Slack alert
execute -n aaaaaa4l5izydl4rfdxv5vmxrbdtkqka5htfq55d2d6pchqcplqv5gjbma -m send_alert -i '{"alert_type":"PUMP_DUMP","severity":"CRITICAL","symbol":"ICICI","entity_id":"ENT-0005","description":"Coordinated pump and dump pattern detected","risk_score":95}'
```

---

## Workflow 6: Trading Window Violation Check

**Scenario**: Designated person trading during blackout

### Natural Language Flow
1. "Is trading window open for RELIANCE?"
2. "Get company insiders for RELIANCE"
3. "Check if Rajesh traded during closed window"
4. "Get Rajesh's UPSI access history"
5. "Generate compliance scorecard"

### Execute Commands
```bash
# Step 1: Check trading window
execute -n aaaaaa3su7z5oaqrgs7757xyzpzp4kxi4v2uyihzf6jpjtlu7kve7ifxfi -m get_trading_window -i '{"company_symbol":"RELIANCE"}'

# Step 2: Get insiders
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m get_company_insiders -i '{"company_symbol":"RELIANCE"}'

# Step 3: Check window violation
execute -n aaaaaa3su7z5oaqrgs7757xyzpzp4kxi4v2uyihzf6jpjtlu7kve7ifxfi -m check_window_violation -i '{"entity_id":"Rajesh Kumar","company_symbol":"RELIANCE","trade_timestamp":1737225600000}'

# Step 4: Get access history
execute -n aaaaaa3su7z5oaqrgs7757xyzpzp4kxi4v2uyihzf6jpjtlu7kve7ifxfi -m get_access_by_person -i '{"accessor_entity_id":"Rajesh Kumar","days_back":30}'

# Step 5: Generate scorecard
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m generate_compliance_scorecard -i '{"entity_id":"Rajesh Kumar","period":"Q4-2025"}'
```

---

## Workflow 7: Volume Anomaly Investigation

**Scenario**: Unusual trading volume detected

### Natural Language Flow
1. "Analyze volume for SBIN"
2. "Check volume anomaly"
3. "Plot volume chart for SBIN"
4. "Get large orders above 1M"
5. "Notify compliance team"

### Execute Commands
```bash
# Step 1: Analyze volume
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m analyze_volume -i '{"symbol":"SBIN"}'

# Step 2: Detect anomaly
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m detect_volume_anomaly -i '{"symbol":"SBIN"}'

# Step 3: Plot volume (plottable)
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m plot_volume_chart -i '{"symbols":"SBIN","days_back":7}'

# Step 4: Get large orders
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m get_large_orders -i '{"min_value":1000000}'

# Step 5: Send message
execute -n aaaaaa4l5izydl4rfdxv5vmxrbdtkqka5htfq55d2d6pchqcplqv5gjbma -m send_message -i '{"channel":"#surveillance-alerts","message":"⚠️ Volume anomaly detected on SBIN - requires immediate review"}'
```

---

## Workflow 8: Entity Risk Assessment

**Scenario**: Full due diligence on suspicious entity

### Natural Language Flow
1. "Search for entity Priya Sharma"
2. "Get their relationships"
3. "Check insider status for TCS"
4. "Get their trading history"
5. "Generate entity risk report"
6. "Create investigation ticket"

### Execute Commands
```bash
# Step 1: Search entity
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m search_entities -i '{"search_query":"Priya Sharma","limit":5}'

# Step 2: Get relationships
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m get_relationships -i '{"entity_id":"Priya Sharma"}'

# Step 3: Check insider status
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m check_insider_status -i '{"entity_id":"Priya Sharma","company_symbol":"TCS"}'

# Step 4: Get account profile
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m get_account_profile -i '{"account_id":"Priya Sharma"}'

# Step 5: Generate risk report
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m generate_entity_risk_report -i '{"entity_id":"Priya Sharma"}'

# Step 6: Create ticket
execute -n aaaaaaz5hqfunhcpxhwzf5nplsgtxaydfgupn5u2at47tkz2igw7ipaya4 -m create_case_ticket -i '{"case_id":"CASE-005","subject_entity":"Priya Sharma","case_summary":"Entity risk assessment - potential insider trading concern","priority":"Medium"}'
```

---

## Workflow 9: Daily Surveillance Summary

**Scenario**: End-of-day surveillance report

### Natural Language Flow
1. "Generate today's surveillance report"
2. "Get pending STRs"
3. "Generate GSM report"
4. "Send daily summary to Slack"

### Execute Commands
```bash
# Step 1: Generate surveillance report
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m generate_surveillance_report -i '{"from_date":"2026-01-18","to_date":"2026-01-18","report_type":"DAILY"}'

# Step 2: Get pending STRs
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m get_pending_strs -i '{"limit":10}'

# Step 3: Generate GSM report
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m generate_gsm_report -i '{"report_date":"2026-01-18"}'

# Step 4: Send daily summary
execute -n aaaaaa4l5izydl4rfdxv5vmxrbdtkqka5htfq55d2d6pchqcplqv5gjbma -m send_daily_summary -i '{"date":"2026-01-18","total_alerts":15,"critical_alerts":3,"open_cases":7,"new_cases":2}'
```

---

## Workflow 10: Related Party Transaction Analysis

**Scenario**: Detect trading between connected entities

### Natural Language Flow
1. "Get connected entities for Mukesh Ambani"
2. "Get trades for all connected accounts"
3. "Check if any traded during closed window"
4. "Are Mukesh and Neeta connected?"
5. "Create compliance case"

### Execute Commands
```bash
# Step 1: Get connected entities
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m get_connected_entities -i '{"entity_id":"Mukesh Ambani","max_hops":2}'

# Step 2: Get trades by accounts
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m get_trades_by_accounts -i '{"account_ids":"Mukesh Ambani,Neeta Ambani,Isha Ambani","symbol":"RELIANCE"}'

# Step 3: Check window violation
execute -n aaaaaa3su7z5oaqrgs7757xyzpzp4kxi4v2uyihzf6jpjtlu7kve7ifxfi -m check_window_violation -i '{"entity_id":"Neeta Ambani","company_symbol":"RELIANCE","trade_timestamp":1737225600000}'

# Step 4: Check connection
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m are_entities_connected -i '{"entity_id_1":"Mukesh Ambani","entity_id_2":"Neeta Ambani","max_hops":1}'

# Step 5: Create case
execute -n aaaaaaz5hqfunhcpxhwzf5nplsgtxaydfgupn5u2at47tkz2igw7ipaya4 -m create_case_ticket -i '{"case_id":"CASE-006","subject_entity":"Ambani Family","case_summary":"Related party transaction analysis - RELIANCE","priority":"Medium"}'
```

---

## Workflow 11: UPSI Leakage Investigation

**Scenario**: Information leak before major announcement

### Natural Language Flow
1. "Get UPSI details for merger announcement"
2. "Who accessed this UPSI?"
3. "Get trades before announcement date"
4. "Check entity relationships"
5. "Generate STR for suspicious access"
6. "Alert compliance team"

### Execute Commands
```bash
# Step 1: Get UPSI
execute -n aaaaaa3su7z5oaqrgs7757xyzpzp4kxi4v2uyihzf6jpjtlu7kve7ifxfi -m get_upsi -i '{"upsi_id":"UPSI-MERGER-001"}'

# Step 2: Get accessors
execute -n aaaaaa3su7z5oaqrgs7757xyzpzp4kxi4v2uyihzf6jpjtlu7kve7ifxfi -m get_upsi_accessors -i '{"upsi_id":"UPSI-MERGER-001"}'

# Step 3: Check UPSI access before date
execute -n aaaaaa3su7z5oaqrgs7757xyzpzp4kxi4v2uyihzf6jpjtlu7kve7ifxfi -m check_upsi_access_before -i '{"entity_id":"ENT-0010","company_symbol":"RELIANCE","before_timestamp":1737225600000}'

# Step 4: Get relationships
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m get_relationships -i '{"entity_id":"ENT-0010"}'

# Step 5: Generate STR
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m generate_str -i '{"case_id":"CASE-007","entity_id":"ENT-0010","suspicious_activity_type":"UPSI_MISUSE","suspicion_reason":"Traded before merger announcement with UPSI access"}'

# Step 6: Slack alert
execute -n aaaaaa4l5izydl4rfdxv5vmxrbdtkqka5htfq55d2d6pchqcplqv5gjbma -m send_alert -i '{"alert_type":"INSIDER","severity":"CRITICAL","symbol":"RELIANCE","entity_id":"ENT-0010","description":"UPSI leakage suspected - merger info accessed before trading","risk_score":98}'
```

---

## Workflow 12: Cross-Symbol Manipulation

**Scenario**: Coordinated trading across multiple stocks

### Natural Language Flow
1. "Analyze volume for RELIANCE, TCS, INFY"
2. "Plot price history comparison"
3. "Get top traders across all three"
4. "Check for common entities"
5. "Send workflow complete notification"

### Execute Commands
```bash
# Step 1: Analyze RELIANCE
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m analyze_volume -i '{"symbol":"RELIANCE"}'

# Step 2: Plot multi-symbol price
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m plot_price_history -i '{"symbols":"RELIANCE,TCS,INFY","days_back":30}'

# Step 3: Get top traders RELIANCE
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m get_top_traders -i '{"symbol":"RELIANCE","limit":10}'

# Step 4: Check entity connection
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m are_entities_connected -i '{"entity_id_1":"ACC001","entity_id_2":"ACC002","max_hops":3}'

# Step 5: Workflow complete
execute -n aaaaaa4l5izydl4rfdxv5vmxrbdtkqka5htfq55d2d6pchqcplqv5gjbma -m send_workflow_complete -i '{"workflow_id":"WF-012","workflow_type":"MANIPULATION_CHECK","result_summary":"Cross-symbol analysis complete - 2 suspicious entities identified","alert_count":2}'
```

---

## Workflow 13: Ticket Management Flow

**Scenario**: Full ticket lifecycle

### Natural Language Flow
1. "Create a ticket for SBIN investigation"
2. "Get ticket details"
3. "Add comment about initial findings"
4. "Update status to In Progress"
5. "Send case update to team"

### Execute Commands
```bash
# Step 1: Create ticket
execute -n aaaaaaz5hqfunhcpxhwzf5nplsgtxaydfgupn5u2at47tkz2igw7ipaya4 -m create_ticket -i '{"summary":"SBIN Volume Anomaly Investigation","description":"Unusual volume spike detected on 2026-01-18","priority":"High"}'

# Step 2: Get ticket
execute -n aaaaaaz5hqfunhcpxhwzf5nplsgtxaydfgupn5u2at47tkz2igw7ipaya4 -m get_ticket -i '{"ticket_key":"WIEL-101"}'

# Step 3: Add comment
execute -n aaaaaaz5hqfunhcpxhwzf5nplsgtxaydfgupn5u2at47tkz2igw7ipaya4 -m add_comment -i '{"ticket_key":"WIEL-101","comment":"Initial analysis: Volume 3x higher than 30-day average. Top 3 accounts identified for review."}'

# Step 4: Update status
execute -n aaaaaaz5hqfunhcpxhwzf5nplsgtxaydfgupn5u2at47tkz2igw7ipaya4 -m update_ticket_status -i '{"ticket_key":"WIEL-101","new_status":"In Progress"}'

# Step 5: Send case update
execute -n aaaaaa4l5izydl4rfdxv5vmxrbdtkqka5htfq55d2d6pchqcplqv5gjbma -m send_case_update -i '{"case_id":"WIEL-101","status":"In Progress","update_message":"Investigation started - reviewing top trading accounts","assigned_to":"Investigator A"}'
```

---

## Workflow 14: Regulatory Compliance Check

**Scenario**: Pre-submission compliance verification

### Natural Language Flow
1. "Generate compliance scorecard for BROKER-Y"
2. "Check their insider status"
3. "Get their trading history"
4. "Generate ESM report"
5. "Submit pending STRs"

### Execute Commands
```bash
# Step 1: Generate scorecard
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m generate_compliance_scorecard -i '{"entity_id":"BROKER-Y","period":"Q4-2025"}'

# Step 2: Check insider status
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m check_insider_status -i '{"entity_id":"BROKER-Y","company_symbol":"HDFC"}'

# Step 3: Get account profile
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m get_account_profile -i '{"account_id":"BROKER-Y"}'

# Step 4: Generate ESM report
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m generate_esm_report -i '{"report_date":"2026-01-18"}'

# Step 5: Submit STR
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m submit_str -i '{"str_id":"STR-001"}'
```

---

## Workflow 15: Multi-Entity Wash Trade Ring

**Scenario**: Circular trading between multiple entities

### Natural Language Flow
1. "Check wash trading ENT-A with ENT-B"
2. "Check wash trading ENT-B with ENT-C"
3. "Are all three connected?"
4. "Get family members of ENT-A"
5. "Create high priority case"
6. "Generate investigation report"

### Execute Commands
```bash
# Step 1: Check A-B
execute -n aaaaaa4s4a4xuzmfsxs5gbs3hcm7npikux3jah52oq6rvnty63jw7qpoam -m detect_wash_trading -i '{"entity_id":"ENT-A","counterparty_id":"ENT-B","symbol":"AXIS","trade_timestamp":1737225600000}'

# Step 2: Check B-C
execute -n aaaaaa4s4a4xuzmfsxs5gbs3hcm7npikux3jah52oq6rvnty63jw7qpoam -m detect_wash_trading -i '{"entity_id":"ENT-B","counterparty_id":"ENT-C","symbol":"AXIS","trade_timestamp":1737225600000}'

# Step 3: Check connection
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m are_entities_connected -i '{"entity_id_1":"ENT-A","entity_id_2":"ENT-C","max_hops":3}'

# Step 4: Get family
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m get_family_members -i '{"entity_id":"ENT-A"}'

# Step 5: Create case
execute -n aaaaaaz5hqfunhcpxhwzf5nplsgtxaydfgupn5u2at47tkz2igw7ipaya4 -m create_case_ticket -i '{"case_id":"CASE-010","subject_entity":"ENT-A/B/C Ring","case_summary":"Circular wash trading ring detected on AXIS","priority":"High"}'

# Step 6: Generate report
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m generate_investigation_report -i '{"case_id":"CASE-010","include_evidence":true}'
```

---

## Workflow 16: Price Chart Analysis

**Scenario**: Technical analysis with visualization

### Natural Language Flow
1. "Plot price history for IBM, AAPL, GOOGL"
2. "Plot volume chart for same stocks"
3. "Get buy/sell ratio for IBM"
4. "Plot top traders for AAPL"

### Execute Commands
```bash
# Step 1: Plot price history
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m plot_price_history -i '{"symbols":"IBM,AAPL,GOOGL","days_back":30}'

# Step 2: Plot volume
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m plot_volume_chart -i '{"symbols":"IBM,AAPL,GOOGL","days_back":7}'

# Step 3: Buy/sell ratio
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m plot_buy_sell_ratio -i '{"symbol":"IBM"}'

# Step 4: Top traders chart
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m plot_top_traders -i '{"symbol":"AAPL","limit":10}'
```

---

## Workflow 17: New Entity Onboarding Check

**Scenario**: Due diligence for new trading account

### Natural Language Flow
1. "Search for entity by PAN ABCDE1234F"
2. "Get entity details"
3. "Check for any existing relationships"
4. "Check insider status across companies"
5. "Generate compliance scorecard"

### Execute Commands
```bash
# Step 1: Search by PAN
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m search_entities -i '{"search_query":"ABCDE1234F","limit":5}'

# Step 2: Get entity
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m get_entity -i '{"entity_id":"NEW-ENT-001"}'

# Step 3: Get relationships
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m get_relationships -i '{"entity_id":"NEW-ENT-001"}'

# Step 4: Check insider status
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m check_insider_status -i '{"entity_id":"NEW-ENT-001","company_symbol":"RELIANCE"}'

# Step 5: Generate scorecard
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m generate_compliance_scorecard -i '{"entity_id":"NEW-ENT-001","period":"Onboarding"}'
```

---

## Workflow 18: Alert Escalation Path

**Scenario**: Critical alert handling with full escalation

### Natural Language Flow
1. "Detect spoofing on NIFTY futures"
2. "Analyze the volume anomaly"
3. "Send critical Slack alert"
4. "Create urgent Jira ticket"
5. "Generate immediate STR"
6. "Send workflow complete notification"

### Execute Commands
```bash
# Step 1: Detect spoofing
execute -n aaaaaa4s4a4xuzmfsxs5gbs3hcm7npikux3jah52oq6rvnty63jw7qpoam -m detect_spoofing -i '{"order_id":"ORD-NIFTY-001","entity_id":"HFT-TRADER-001","symbol":"NIFTY","order_details":"Algo trading pattern detected"}'

# Step 2: Analyze volume
execute -n aaaaaa4s4a4xuzmfsxs5gbs3hcm7npikux3jah52oq6rvnty63jw7qpoam -m analyze_volume_anomaly -i '{"symbol":"NIFTY","interval":"1min"}'

# Step 3: Critical alert
execute -n aaaaaa4l5izydl4rfdxv5vmxrbdtkqka5htfq55d2d6pchqcplqv5gjbma -m send_alert -i '{"alert_type":"SPOOFING","severity":"CRITICAL","symbol":"NIFTY","entity_id":"HFT-TRADER-001","description":"High-frequency spoofing detected on NIFTY futures","risk_score":99}'

# Step 4: Create ticket
execute -n aaaaaaz5hqfunhcpxhwzf5nplsgtxaydfgupn5u2at47tkz2igw7ipaya4 -m create_case_ticket -i '{"case_id":"CASE-URGENT-001","subject_entity":"HFT-TRADER-001","case_summary":"CRITICAL: NIFTY futures spoofing - immediate action required","priority":"High"}'

# Step 5: Generate STR
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m generate_str -i '{"case_id":"CASE-URGENT-001","entity_id":"HFT-TRADER-001","suspicious_activity_type":"SPOOFING","suspicion_reason":"High-frequency order manipulation on NIFTY futures"}'

# Step 6: Workflow complete
execute -n aaaaaa4l5izydl4rfdxv5vmxrbdtkqka5htfq55d2d6pchqcplqv5gjbma -m send_workflow_complete -i '{"workflow_id":"WF-URGENT-001","workflow_type":"CRITICAL_ESCALATION","result_summary":"Critical spoofing alert escalated - STR generated, Jira created","alert_count":1}'
```

---

## Workflow 19: Quarterly Compliance Audit

**Scenario**: End of quarter regulatory reporting

### Natural Language Flow
1. "Generate surveillance report for Q4"
2. "Generate GSM report"
3. "Generate ESM report"
4. "Get all pending STRs"
5. "Send quarterly summary to Slack"

### Execute Commands
```bash
# Step 1: Quarterly surveillance report
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m generate_surveillance_report -i '{"from_date":"2025-10-01","to_date":"2025-12-31","report_type":"QUARTERLY"}'

# Step 2: GSM report
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m generate_gsm_report -i '{"report_date":"2025-12-31"}'

# Step 3: ESM report
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m generate_esm_report -i '{"report_date":"2025-12-31"}'

# Step 4: Get pending STRs
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m get_pending_strs -i '{"limit":50}'

# Step 5: Send summary
execute -n aaaaaa4l5izydl4rfdxv5vmxrbdtkqka5htfq55d2d6pchqcplqv5gjbma -m send_message -i '{"channel":"#compliance-reports","message":"📊 Q4 2025 Compliance Reports Generated\n- Surveillance Report: ✅\n- GSM Report: ✅\n- ESM Report: ✅\n- Pending STRs: Review required"}'
```

---

## Workflow 20: Complete Case Lifecycle

**Scenario**: Full investigation from alert to closure

### Natural Language Flow
1. "Detect front-running for BROKER-Z on KOTAKBANK"
2. "Get entity details and relationships"
3. "Create investigation case"
4. "Generate investigation report"
5. "Close the ticket with resolution"
6. "Send case closure notification"

### Execute Commands
```bash
# Step 1: Detect front-running
execute -n aaaaaa4s4a4xuzmfsxs5gbs3hcm7npikux3jah52oq6rvnty63jw7qpoam -m detect_front_running -i '{"entity_id":"BROKER-Z","symbol":"KOTAKBANK","client_trade_timestamp":1737225600000,"prop_trade_timestamp":1737225590000}'

# Step 2: Get entity and relationships
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m get_relationships -i '{"entity_id":"BROKER-Z"}'

# Step 3: Create case
execute -n aaaaaaz5hqfunhcpxhwzf5nplsgtxaydfgupn5u2at47tkz2igw7ipaya4 -m create_case_ticket -i '{"case_id":"CASE-FINAL-001","subject_entity":"BROKER-Z","case_summary":"Front-running investigation on KOTAKBANK","priority":"High"}'

# Step 4: Generate report
execute -n aaaaaa77wlohisawkkbxkgc77cb24slezi4a5yx6obqiyjcmwofwx3njfm -m generate_investigation_report -i '{"case_id":"CASE-FINAL-001","include_evidence":true}'

# Step 5: Close ticket
execute -n aaaaaaz5hqfunhcpxhwzf5nplsgtxaydfgupn5u2at47tkz2igw7ipaya4 -m close_ticket -i '{"ticket_key":"WIEL-FINAL-001","resolution":"Investigation complete - no violation found after review"}'

# Step 6: Send closure notification
execute -n aaaaaa4l5izydl4rfdxv5vmxrbdtkqka5htfq55d2d6pchqcplqv5gjbma -m send_case_update -i '{"case_id":"CASE-FINAL-001","status":"CLOSED","update_message":"Investigation concluded - cleared after thorough review","assigned_to":"Investigation Team"}'
```

---

## Quick Cache Population Script

Run all these commands sequentially to fully populate the context caches:

```bash
# Populate UPSI cache
execute -n aaaaaa3su7z5oaqrgs7757xyzpzp4kxi4v2uyihzf6jpjtlu7kve7ifxfi -m get_active_upsi -i '{"company_symbol":"RELIANCE"}'
execute -n aaaaaa3su7z5oaqrgs7757xyzpzp4kxi4v2uyihzf6jpjtlu7kve7ifxfi -m check_window_violation -i '{"entity_id":"Rajesh Kumar","company_symbol":"TCS","trade_timestamp":1737225600000}'

# Populate Trade Data cache
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m get_trades_by_symbol -i '{"symbol":"INFY","limit":10}'
execute -n aaaaaa7ycnpwxv2xks67l4lkczhwgbyawt34u7esvsbfgbnq7putxnvmfm -m get_account_profile -i '{"account_id":"Priya Sharma"}'

# Populate Anomaly Detection cache
execute -n aaaaaa4s4a4xuzmfsxs5gbs3hcm7npikux3jah52oq6rvnty63jw7qpoam -m detect_spoofing -i '{"order_id":"ORD-001","entity_id":"ENT-0001","symbol":"HDFC","order_details":"Large order"}'
execute -n aaaaaa4s4a4xuzmfsxs5gbs3hcm7npikux3jah52oq6rvnty63jw7qpoam -m detect_wash_trading -i '{"entity_id":"Mukesh Ambani","counterparty_id":"Mukesh Ambani","symbol":"RELIANCE","trade_timestamp":1737225600000}'

# Populate Entity Relationship cache
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m get_entity -i '{"entity_id":"Neeta Ambani"}'
execute -n aaaaaa36wpz26hhxrmyvo2clmpqqkwqudoqkymfkgltfmtvoceftcfes5u -m check_insider_status -i '{"entity_id":"Amit Patel","company_symbol":"ICICI"}'
```

---

> **Made with ❤️ for Icarus Agentic Workflows**
