# 🔗 Event Correlation – Security Operations Fundamentals (Palo Alto Networks)

> **Event correlation** is the analytical process of linking multiple security events across diverse sources to identify complex threat patterns and high-fidelity alerts. It is the backbone of modern **Security Operations Centers (SOC)** and critical to **attack surface visibility**, **threat hunting**, and **incident response**.

---

## 🎯 Objectives of Event Correlation

- ✅ Reduce noise by aggregating redundant or low-value alerts  
- 🧠 Identify multi-stage attacks (e.g., phishing ➝ privilege escalation ➝ lateral movement)  
- ⏱ Improve Mean Time To Detect (MTTD) and Respond (MTTR)  
- 🚨 Generate contextual, high-confidence alerts for analyst triage

---

## 🧩 Core Components

| Component              | Description |
|------------------------|-------------|
| **Event**              | Raw log or alert from endpoint, firewall, IAM, or application |
| **Correlation Rule**   | Logic to bind multiple related events based on temporal, spatial, or behavioral relationships |
| **Incident**           | A confirmed security event or series of events that require response |
| **Alert**              | A triggered rule indicating possible compromise |
| **Playbook**           | Automated or manual steps to investigate/respond |

---

## ⚙️ Types of Correlation Logic

### 1. **Rule-Based Correlation**
Static, predefined conditions trigger alerts.
```yaml
If > 5 login failures + 1 success within 5 mins from same IP ➝ Brute Force Alert
```

### 2. **Temporal Correlation**

- Events must occur in a defined sequence and timeframe.

Example: Unusual login ➝ file exfiltration ➝ endpoint shutdown within 10 minutes

### 3. **Contextual Correlation**

- Enrich events with:

- User risk score

- Threat Intelligence (TI)

- GeoIP / Asset Criticality

### 4. **Anomaly-Based Correlation**

- Statistical or ML-based outlier detection (UEBA):

User downloads 10× average data volume at 2AM from atypical location

🧪 Example Use Case: Credential Access Detection

Scenario:

A user exhibits signs of credential misuse, potentially due to compromised credentials or insider threat.

| Event Source | Activity                                       |
| ------------ | ---------------------------------------------- |
| `Firewall`   | Login attempt from blacklisted IP              |
| `EDR`        | Credential dump tool detected (e.g., Mimikatz) |
| `SIEM`       | Account privilege escalated to domain admin    |
| `TI Feed`    | IOC match: IP flagged as C2 by IBM X-Force     |

Correlation Rule:

```c
IF
  [TI Match: IP] AND
  [Privilege Escalation] AND
  [Credential Tool Detected]
THEN
  Raise HIGH alert for Account Compromise
```

## 🛠 Platforms That Support Event Correlation

| Platform         | Type            | Correlation Capability  |
| ---------------- | --------------- | ----------------------- |
| **Cortex XSIAM** | XDR/SIEM Fusion | Rule-based + ML-driven  |
| **Splunk**       | SIEM            | Search-time correlation |
| **Elastic SIEM** | Open Source     | Timeline and rule-based |
| **QRadar**       | SIEM            | Flows + Logs + TI       |
| **Cortex XSOAR** | SOAR            | Playbook automation     |

✅ Best Practices

- Write atomic, modular, and stackable correlation rules

- Leverage threat intelligence enrichment (IP/Hash/Domain reputation)

- Include asset context: user role, asset sensitivity

- Continuously tune detection logic to reduce false positives

- Integrate with SOAR for faster triage and automated response

## 🚫 Common Pitfalls

| Pitfall                     | Impact                          |
| --------------------------- | ------------------------------- |
| Overly generic rules        | High false positive rate        |
| No TI integration           | Missed attribution & enrichment |
| Lack of tuning over time    | Degraded detection quality      |
| No context or playbook tied | Analyst burnout                 |



