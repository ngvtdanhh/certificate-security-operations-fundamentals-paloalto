# 🤖 SOAR Playbook – Automated Threat Containment & Enrichment

This document outlines a sample SOAR playbook used for automating the response to high-confidence malware alerts in enterprise environments.

---

## 🧭 Use Case

**Alert Type**: Malware detected by Cortex XDR on a workstation  
**Confidence Level**: High  
**Objective**: Contain host and enrich alert with threat intelligence

---

## 🧩 Playbook Steps

| Step | Action                                   | Tool/Integration        |
|------|------------------------------------------|-------------------------|
| 1️⃣   | Ingest alert from XDR                    | XDR integration         |
| 2️⃣   | Check host reputation via VirusTotal     | Threat Intel API        |
| 3️⃣   | If score ≥ 80, isolate endpoint          | Cortex XDR API          |
| 4️⃣   | Extract indicators from alert (hash, IP) | Regex / Parsing Engine  |
| 5️⃣   | Submit indicators to Threat Intelligence | AutoFocus / MISP        |
| 6️⃣   | Notify SOC via Slack/Email               | Messaging Integration   |
| 7️⃣   | Create incident ticket in Jira           | ITSM integration        |

---

## 💡 Logic Conditions

- **IF** `malware_confidence_score >= 80`  
- **AND** `endpoint not already isolated`  
- → Proceed with auto-isolation

- **ELSE IF** alert marked as “low confidence”  
- → Assign to SOC Level 1 for manual triage

---

## 📉 Sample Output

```json
{
  "host": "WORKSTATION-002",
  "malware_name": "Win32.Meterpreter",
  "verdict": "High Confidence",
  "action": "Host Isolated, TI submitted, SOC Notified"
}
```

## 🔐 Security Controls

- Role-based execution (SOC Tier 2+ only)

- Auto-disable playbook after 3 consecutive errors

- All actions logged in SIEM and ticketing system

## 🧠 Why It Matters

- Reduces MTTR (Mean Time to Respond) significantly

- Limits lateral movement in active attacks

- Empowers SOC teams to focus on higher-level threats

## 🧰 Tools Used

- Cortex XSOAR / XDR

- VirusTotal API

- MISP / AutoFocus

- Jira, Slack, Microsoft Teams

## 📚 References

- Palo Alto: Security Operations Fundamentals (SOAR Modules)

- Cortex XSOAR Playbook Library

- MITRE D3FEND Framework for Response Patterns

```yaml
“Automation is not about replacing analysts — it's about giving them more time to think critically.”
```
