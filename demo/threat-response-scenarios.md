# ⚙️ Threat Response Scenarios – SOC Automation Demos

This file includes practical simulations of threat response workflows using industry-standard tools such as Cortex XSOAR, SIEM systems, and scripting techniques. These demos reinforce real-world incident handling aligned with the Security Operations Fundamentals course by Palo Alto Networks.

---

## 🚨 Scenario 1: Auto-Isolation of Infected Endpoint

**Objective**: Automatically isolate an endpoint exhibiting suspicious beaconing behavior detected by an EDR.

**Tooling**:
- Cortex XSOAR
- Cortex XDR
- Slack for analyst notifications

**Workflow**:

```bash
1. XDR Alert: DNS Beacon activity detected
2. SOAR verifies alert confidence score > 90%
3. Check threat intel (VirusTotal, internal TI feed)
4. If IOC matches known threat → auto-isolate endpoint
5. Send real-time Slack notification to L1/L2 SOC
```

Example Playbook JSON:

```json

{
  "playbook": "Auto_Isolate_Host",
  "trigger": "XDR Alert: DNS Beacon",
  "actions": [
    "Verify Alert",
    "Check Threat Intel",
    "Isolate Endpoint",
    "Notify SOC"
  ]
}
```

## 🧪 Scenario 2: Phishing Email IOC Extraction

- Objective: Extract URLs from a reported phishing email and submit to threat intelligence platforms.

Steps:

```python
# demo/phishing_ioc_extractor.py
import re
email = open("samples/reported_email.eml").read()
urls = re.findall(r"https?://[\\w./%-]+", email)
print("Extracted URLs:", urls)
```

## Next Actions:

- Submit each URL to VirusTotal or Hybrid Analysis

- Correlate in SIEM for similar traffic patterns

- Block malicious domains on firewall/proxy

## 🔁 Scenario 3: IOC Propagation via MISP

- Objective: Share high-confidence IOCs to multiple platforms (EDR, FW, SIEM) using MISP API.

MISP Workflow:

```bash
POST /events { "ioc": "malicious.com", "type": "domain", "threat_level": 3 }
→ Forward to Cortex XDR, Palo Alto FW, Splunk
→ Auto-tag future events with this IOC
```

## 🧯 Scenario 4: Insider Threat – Unauthorized Access to HR Files

- Detection:

Splunk detects access to /hr/confidential from unauthorized user

- Response:

Disable account in Active Directory

Archive audit logs

Alert HR & Security team

Initiate post-incident review

SIEM Search:

```spl
index=auth_logs sourcetype=linux_secure
\"/hr/confidential\" AND user!=\"hr_group\" | stats count by user, src_ip
```

## 🧠 Analyst Takeaways

- Automating isolation and IOC handling increases MTTR efficiency

- Regex parsing, TI lookups, and SIEM correlation are vital daily tasks

- SOAR platforms (like XSOAR) drastically improve triage consistency

- Documentation and repeatable playbooks are essential in SOC

