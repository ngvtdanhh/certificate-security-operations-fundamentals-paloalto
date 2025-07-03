# 📊 SIEM and Alerts – Security Operations Fundamentals (Palo Alto Networks)

> **SIEM (Security Information and Event Management)** platforms collect, normalize, and analyze log data to detect threats in real-time. Alerts are the output of detection logic and are the foundation of SOC triage and response workflows.

---

## 🧠 SIEM Overview

A **SIEM** solution provides:

- 🗃️ **Centralized log collection** from endpoints, firewalls, servers, cloud apps  
- 🔎 **Correlation and detection logic** across data sources  
- 🧠 **Threat intelligence enrichment**  
- ⏰ **Real-time alerting and notification**  
- 📈 **Dashboards & reporting** for visibility and compliance

### 🔗 SIEM vs XDR

| Feature              | SIEM                          | XDR                               |
|----------------------|-------------------------------|------------------------------------|
| Scope                | Broad (logs, flows, TI, apps) | Focused (endpoint + network + cloud) |
| Detection Logic      | Rule-based + correlation      | Behavioral + ML + telemetry fusion |
| Investigation UX     | Traditional log queries       | Integrated timeline + context      |
| Examples             | Splunk, QRadar, ArcSight      | Cortex XDR, SentinelOne Singularity |

---

## 🚨 What is an Alert?

An **alert** is a security signal raised when specific detection rules or anomalies are triggered.

### 🧩 Alert Components

| Field             | Description                                  |
|------------------|----------------------------------------------|
| Timestamp         | When the alert was generated                 |
| Severity          | Informational, Low, Medium, High, Critical   |
| MITRE Mapping     | Tactic/Technique associated (e.g., TA0006)   |
| Source IP/User    | Actor or system involved                     |
| Rule Name/ID      | The detection rule that generated the alert  |
| Enrichment        | TI, asset tag, prior activity                |
| Disposition       | True Positive / False Positive / Benign      |

---

## 🏗️ How SIEM Builds Alerts

### 1. **Data Ingestion**
- Logs from:
  - Firewalls
  - EDR/NDR tools
  - IAM & SSO platforms
  - DNS/DHCP/Proxy

### 2. **Parsing & Normalization**
- Convert diverse formats into a unified schema (e.g., ECS, CIM)

### 3. **Correlation Rules / Detections**
- Rule examples:
```yaml
- Multiple login failures + success from new geo ➝ Brute Force
- DNS beaconing to DGA domains ➝ Malware Infection
- File write in C:\Windows\Temp + PowerShell spawn ➝ Suspicious Activity
```
### 4. **Alert Generation & Triage**

Routed to analysts via:

- Dashboards (Splunk, XDR)

- Email / Slack

- SOAR queue (e.g., Cortex XSOAR, TheHive)

## 🔍 Alert Lifecycle (SOC Perspective)
 
 ```mermaid 
flowchart LR
A[Alert Raised] --> B[Triage by Analyst]
B --> C{Valid Threat?}
C -- Yes --> D[Investigate Context]
C -- No --> E[Mark as False Positive]
D --> F[Escalate / Contain]
F --> G[Document & Close]
E --> G
```

## 📏 Alert Quality Metrics

| Metric                      | Why It Matters                   |
| --------------------------- | -------------------------------- |
| True Positive Rate (TPR)    | Accuracy of detections           |
| False Positive Rate (FPR)   | Analyst fatigue, wasted time     |
| MTTD – Mean Time to Detect  | Speed of threat identification   |
| MTTR – Mean Time to Respond | Speed of containment/eradication |
| Alert Volume per Analyst    | Operational load / alert fatigue |

## ⚠️ Common Pitfalls

| Issue                       | Impact                                |
| --------------------------- | ------------------------------------- |
| Overly verbose rules        | High alert volume, fatigue            |
| No threat intel integration | Missed context, low confidence alerts |
| Siloed logs (no EDR/NDR)    | Blind spots in detection              |
| Static rules only           | Misses evolving or unknown threats    |

## 🔧 Optimization Techniques

🧠 Integrate MITRE ATT&CK mappings for context

🧹 Regularly tune rules to reduce false positives

🌐 Enrich alerts with GeoIP, asset criticality, TI

⚙️ Leverage SOAR to auto-close benign alerts

## 🧰 SIEM Tools Comparison

| Platform         | Strength                      | Limitation                       |
| ---------------- | ----------------------------- | -------------------------------- |
| **Splunk**       | Powerful search, flexible SPL | Expensive, complex tuning        |
| **QRadar**       | Flow + log integration        | UI and customization limitations |
| **Elastic SIEM** | Open-source, scalable         | Needs tuning, weak correlation   |
| **Cortex XSIAM** | Built-in detection + response | Newer in traditional SIEM space  |

## 📚 References

- Palo Alto Networks – Security Operations Fundamentals (2025)

- MITRE ATT&CK – Detection Mapping and Adversary Techniques

- Splunk/Elastic Docs – SIEM Tuning and Alert Logic

- NIST SP 800-61 – Incident Handling Lifecycle

## 🧪 Validate rules with test datasets (e.g., Atomic Red Team, Sigma)

## 📌 Summary

SIEM and alerting form the core detection engine of any security operations strategy. Well-tuned alert logic combined with contextual enrichment empowers defenders to act swiftly and decisively.

```yaml
"An alert is only as useful as the context it carries." – SOC Principle
```
