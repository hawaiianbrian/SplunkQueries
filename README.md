# SplunkQueries

A collection of Splunk searches and detection use cases for security monitoring, threat hunting, and SOC dashboard development.

This repository focuses on identifying real-world attacker behaviors across identity, endpoint, email, and network activity.

---

## Overview

These queries are designed to support:

* Threat hunting
* Detection engineering
* SOC dashboards
* Incident response and triage
* Security visibility and gap analysis

Each detection is documented with:

* Purpose
* Splunk query
* Use case
* Investigation context

---

## Detection Coverage

This repository provides visibility across multiple stages of the attack lifecycle:

* Initial Access (phishing, RDP, VPN anomalies)
* Execution (suspicious processes, LOLBins)
* Persistence (autoruns, mailbox rules, service accounts)
* Privilege Escalation (admin creation, escalation activity)
* Defense Evasion (log clearing, obfuscation)
* Credential Access (brute force, MFA abuse)
* Lateral Movement (remote execution tools, admin logons)
* Exfiltration (data spikes, TOR, email abuse)

---

## Query Categories

### Identity and Authentication

* AccountDeleted-24hrCreation.md
* Disabled-Account-ReEnabled.md
* Failed-Attempt-Logon-DisableAccount.md
* Failed-Auth-NonAccount.md
* Failed-RDP-Logon.md
* GeoTravelImpossible.md
* MFAfailure.md
* Successful-Logons.md
* Username-Bruteforce-Guess.md
* VPN-Connections
* Windows-LastPW-Reset.md

---

### Endpoint and EDR

* AutoRun-EDR-Detect.md
* Cleared-Windows-Logs.md
* Crowdstrike-Bruteforce-Attempts.md
* Crowdstrike-ParentChild-Processes.md
* Crowdstrike-USB-Search.md
* File-Deletion-Attempts.md
* RemoteExecTool.md
* SVCaccountAbuse.md
* Suspicious-Process-Creations.md

---

### Email and Messaging

* Harmony-Avanan-Suspicious-URLSattachments.md
* InboxMassDelete.md
* MailboxRule-Create.md
* Mailserver-Changes.md
* Move-to-RSSfolders.md
* Outgoing-50plus-Recipients.md
* Possible-Spear-Phishing.md

---

### Network and Firewall

* BeaconingDetection.md
* DataExfilDetect.md
* Fortigate-Modifications.md
* Tor-Connections.md

---

### Privilege and Access

* AdminLogons-NonAdminSystems.md
* New-Local-Admin-Accounts.md
* Privilege-Escalation-Detection.md

---

### System and Monitoring

* MSexchange-Errors.md
* Successful-File-Access.md
* User-LogONoff-Duration.md
* Last-15m.md

---

## Example Detection

### Failed RDP Logon

Detects repeated failed Remote Desktop Protocol (RDP) logon attempts, which may indicate brute-force activity or unauthorized access attempts against exposed systems.

```spl
index=wineventlog EventCode=4625 LogonType=10
| stats count by _time, host, user, src_ip
| sort - count
```

Why it matters:
Repeated failed RDP logons can indicate password spraying, brute-force attacks, or early-stage attacker access attempts.

---

## Log Sources

These queries may rely on one or more of the following:

* Windows Event Logs
* Sysmon
* CrowdStrike Falcon
* SentinelOne
* Microsoft 365 / O365
* Azure / Entra ID sign-in logs
* Exchange logs
* Firewall and proxy logs
* VPN logs
* DNS logs
* Email security platforms such as Avanan

Field names, indexes, and sourcetypes may vary by environment.

---

## Tuning Guidance

Before using any query in production:

1. Validate indexes and sourcetypes
2. Confirm field mappings
3. Filter known benign activity
4. Apply thresholds where necessary
5. Test against historical data

---

## Goals

* Standardize Splunk search development
* Improve detection documentation
* Reduce duplicate effort
* Build reusable dashboards and alerts
* Track security monitoring maturity over time

---

## Contributing

When adding a new query, include:

* Detection name
* Description and purpose
* Splunk search
* Data source dependencies
* Known false positives
* Tuning recommendations
* Explanation of why the detection matters

---

## Disclaimer

These queries are baseline examples and should be validated and tuned before production use.
