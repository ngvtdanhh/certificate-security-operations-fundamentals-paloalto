# 🎯 SIEM Rule Tuning – Reducing False Positives in Security Operations

This file outlines practical strategies and examples for tuning SIEM detection rules to reduce alert fatigue, improve detection precision, and streamline SOC workflows.

---

## 🧩 Problem: Excessive Failed Login Alerts

**Rule**:  
```spl
index=windows_logs sourcetype="WinEventLog:Security"
EventCode=4625
| stats count by user, src_ip
| where count > 10
```

Issue:

- Triggers on service accounts, dev environments, or known vulnerability scans

- Causes 50+ false alerts/day

## 🛠️ Tuning Strategy

| Step               | Description                                                     |
| ------------------ | --------------------------------------------------------------- |
| ✅ Add allowlist    | Exclude trusted IPs, accounts                                   |
| ⏱️ Add time window | Limit to X attempts within Y minutes                            |
| 🧠 Add logic       | Require unique `src_ip` or diverse users to increase confidence |

Updated Rule Example:

```spl
index=windows_logs sourcetype="WinEventLog:Security" EventCode=4625
| where user!="svc_backup" AND src_ip!="192.168.1.10"
| bucket _time span=10m
| stats dc(src_ip) AS unique_sources, count BY user, _time
| where count > 10 AND unique_sources > 3
```

## 🧪 Use Case: PowerShell Abuse Detection

Original Rule:

```spl
index=sysmon EventCode=1 Image="*powershell.exe*"
```

Refined:

```spl
index=sysmon EventCode=1
| regex CommandLine="(?i)(Invoke-WebRequest|IEX|DownloadString|Base64)"
| table _time user CommandLine host
```

Outcome:

- Removes legitimate PowerShell scripts

- Focuses on known abuse patterns

## 📉 Measured Results

| Metric              | Before Tuning | After Tuning |
| ------------------- | ------------- | ------------ |
| Daily Alerts        | 80            | 22           |
| False Positive Rate | \~60%         | <15%         |
| Analyst Review Time | \~2.5 hours   | \~45 mins    |

## ✍️ Best Practices

- Review false positives weekly

- Maintain allowlists in a central place (e.g., lookup tables)

- Involve threat intel team for behavior-based tuning

- Document tuning rationale in your SOC Wiki or XSOAR platform

## 📚 References

- Palo Alto – Security Operations Fundamentals (SIEM module)

- Splunk Use Case Library: docs.splunk.com

- MITRE ATT&CK mappings for alert enrichment





