# 🚨 Incident Escalation Framework – SOC Playbook

This document outlines a structured escalation model for handling incidents in a multi-tiered Security Operations Center (SOC). It defines what qualifies for escalation, timelines, and communication standards between levels.

---

## 🎯 Purpose

- Ensure timely and appropriate escalation of threats
- Avoid burnout from alert overload or misrouting
- Improve Mean Time to Respond (MTTR) and containment quality

---

## 🧱 Escalation Tiers

| Tier | Role                            | Escalation Trigger                           |
|------|----------------------------------|----------------------------------------------|
| L1   | Alert Triage, IOC Correlation   | Unfamiliar behavior, policy violation         |
| L2   | Root Cause, Host & Net Forensics| Malware lateral movement, persistence signs   |
| L3   | Threat Hunt, Deep IR            | APT tactics, 0-day, widespread compromise     |

---

## 📌 When to Escalate?

### 🔍 L1 → L2

- Alert from SIEM or XDR lacks full context
- Alert involves privilege escalation or internal lateral movement
- Evidence of data exfiltration or command & control (C2) behavior

### 🔐 L2 → L3

- Attribution linked to nation-state/APT groups
- Incident crosses compliance/regulatory boundaries (e.g., PCI, HIPAA)
- Tools/tactics match MITRE TTPs (e.g., Mimikatz, PSExec)

---

## 📞 Communication Channels

| Tier | Communication Medium       | Notes                             |
|------|-----------------------------|------------------------------------|
| L1   | Ticketing System + Slack    | Include IOC summary and screenshots |
| L2   | Internal IR Tracker + Call | Escalate with annotated timeline   |
| L3   | Security Bridge Call       | Include execs if business impact   |

---

## 🕒 Escalation SLA (Time-Based)

| Severity Level | Escalation Deadline   |
|----------------|------------------------|
| Critical       | ≤ 10 minutes           |
| High           | ≤ 30 minutes           |
| Medium         | ≤ 1 hour               |
| Low            | Within shift cycle     |

> 🕹 All escalations must include incident ID, IOC summary, confidence level, and any containment actions taken.

---

## 📑 Escalation Checklist

- [ ] Confirm alert is **not** a false positive
- [ ] Enrich with asset criticality (from CMDB)
- [ ] Attach logs, packet captures, screenshots
- [ ] Provide working hypothesis
- [ ] List tools/scripts already run

---

## 📚 References

- **Security Operations Fundamentals – Palo Alto**
- NIST 800-61: Computer Security Incident Handling
- SANS Blue Team Handbook
- SOC-CMM (Capability Maturity Model)

---

> **“Escalation without clarity is escalation failure.”**

