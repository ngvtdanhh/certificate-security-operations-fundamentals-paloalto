# 🛡️ Blue Team Strategy Playbook – SOC Perspective

This strategic document outlines the layered defensive tactics, detection priorities, and triage standards adopted by Blue Teams in modern SOC (Security Operations Centers).

---

## 🎯 Objectives

- Establish SOC operational standards
- Define tiered response models (L1 → L3)
- Prioritize alerts and threat intelligence integration
- Create repeatable, measurable defense routines

---

## 🧱 1. Defensive Layers (Defense-in-Depth)

| Layer            | Examples                             | Tools Used                      |
|------------------|--------------------------------------|----------------------------------|
| 🧍 Endpoint       | EDR, AV, Isolation Protocols          | Cortex XDR, Defender ATP         |
| 🌐 Network        | IDS/IPS, Flow Monitoring              | Zeek, Suricata, NetFlow          |
| 🔒 Identity       | MFA, Privilege Escalation Detection   | Okta, AD Audit, IAM Logs         |
| 🛠 Application     | WAF, App Behavior Analysis             | Palo Alto NGFW, Runtime Sensors  |
| ☁️ Cloud          | Misconfiguration Alerts, CSPM         | Prisma Cloud, AWS GuardDuty      |

---

## 🔎 2. Alert Prioritization Framework

| Alert Source     | Default Severity | Auto Escalation Condition           |
|------------------|------------------|-------------------------------------|
| XDR: Malware      | High              | Malware score > 80 or lateral signs |
| SIEM: Brute Force | Medium            | >20 failed logins in 5 min          |
| UEBA: Behavior Anomaly | Low        | Rare location + admin access        |
| Threat Intel: IOC Match | Critical   | IOC from nation-state APT          |

---

## ⚙️ 3. SOC Tier Functions

| Tier   | Role Description                       | Escalation Criteria         |
|--------|-----------------------------------------|-----------------------------|
| L1     | Triage, enrichment, validation          | Unknown behavior, confirmed malware |
| L2     | Root cause, lateral analysis            | Signs of persistence or pivoting   |
| L3     | Threat hunting, IR coordination         | APT-level tactics, deep forensics  |

---

## 🧠 4. Threat Intel Integration Pipeline

- 🔄 Daily STIX/TAXII feeds pulled from MISP and IBM X-Force
- 🧮 Enrichment of IOCs with AutoFocus & VirusTotal
- 🎯 Real-time correlation via Cortex XSOAR into SIEM

> TI scores >= 80 automatically tagged `malicious`  
> New IOCs with unknown confidence go to threat hunting backlog

---

## 📘 5. Incident Lifecycle (Palo Alto Model)

[ DETECT ] → [ VALIDATE ] → [ CONTAIN ] → [ ERADICATE ] → [ RECOVER ] → [ REVIEW ]

Each phase involves defined checklists, tickets, and response logs to ensure completeness and auditability.

---

## 🧩 Metrics to Monitor

| Metric                 | Description                          |
|------------------------|--------------------------------------|
| MTTA (Time to Acknowledge) | Time from alert → analyst open   |
| MTTR (Time to Respond)     | Time to contain or remediate     |
| Escalation Ratio           | % of L1 alerts needing L2+        |
| False Positive Rate        | Total benign alerts flagged       |

---

## 📚 References

- **Security Operations Fundamentals – Palo Alto**
- MITRE ATT&CK and D3FEND models
- “The Blue Team Field Manual (BTFM)”
- NIST SP 800-61 – Computer Security Incident Handling Guide
