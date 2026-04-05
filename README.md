# Security Monitoring & Log Analysis Lab

## 🚨 Attack Scenario

This lab simulates a brute-force authentication attack against a Linux system, followed by successful access and privilege escalation using sudo.

An attacker performs repeated failed login attempts targeting multiple usernames before successfully authenticating and executing elevated commands.

The objective is to detect and analyze this multi-stage attack using Splunk SIEM.

## Overview
This project demonstrates security monitoring and log analysis using Linux authentication logs and Splunk Enterprise.

## Objectives
- Analyze Linux authentication logs
- Identify failed login attempts and suspicious behavior
- Perform SIEM-based event analysis in Splunk
- Correlate events by source IP, targeted username, and command activity
- Identify indicators of compromise (IOCs)

## Tools Used
- Splunk Enterprise
- Ubuntu WSL
- Linux authentication logs (`/var/log/auth.log`)
- grep
- Regular expressions (regex)

## Key Activities
- Ingested and reviewed log data
- Developed custom Splunk queries to detect brute-force authentication patterns and privilege escalation activity
- Correlated events across logs to detect suspicious behavior
- Investigated potential security incidents based on log evidence

## Project Structure
- `/logs` – Sample log files used for analysis  
- `/queries` – Search queries used to detect events  
- `/screenshots` – Evidence of analysis and findings  

## 🔍 Detection Approach

The following detection strategy was used to identify malicious activity:

- Detect repeated failed login attempts indicating brute-force behavior
- Identify successful authentication events following failed attempts
- Correlate activity by source IP and targeted usernames
- Detect privilege escalation through sudo command execution
- Reconstruct attacker behavior across multiple log events

## SIEM Setup

Splunk Enterprise was installed locally and used to ingest authentication logs for analysis. The logs were uploaded via the Splunk "Add Data" interface and indexed for querying.

## SIEM Analysis (Splunk)

Authentication logs were ingested into Splunk Enterprise to simulate real-world Security Operations Center (SOC) monitoring and detection workflows. Analysis focused on identifying failed login attempts, correlating attack patterns, and detecting privilege escalation activity.

### Failed Login Events (Initial Detection)
The following search identifies failed authentication attempts within the dataset.

```spl
"Failed password"
```

![Splunk Failed Logins](screenshots/splunk-failed-logins.png)

### Failed Login Summary by Source IP
This query extracts source IP addresses and aggregates failed login attempts to identify potential attack sources.

```spl
"Failed password"
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip
```

![Splunk Failed by IP](screenshots/splunk-failed-by-ip.png)

### Failed Login Summary by Targeted Username
This query extracts targeted usernames and aggregates failed login attempts to identify which accounts are being targeted.

```spl
"Failed password"
| rex "invalid user (?<target_user>\w+)"
| stats count by target_user
```

![Splunk Failed by User](screenshots/splunk-failed-by-user.png)

### Sudo Command Summary (Privilege Escalation)
This query extracts and summarizes commands executed with elevated privileges, providing visibility into administrative activity.

```spl
sudo "COMMAND="
| rex "COMMAND=(?<command>.+)$"
| stats count by command
```

![Splunk Sudo Commands](screenshots/splunk-sudo-commands.png)

## 🔍 Key Findings

- Detected brute-force attack activity originating from multiple source IP addresses  
- Identified targeted usernames including admin, root, and test accounts  
- Observed successful authentication following repeated failed login attempts  
- Detected privilege escalation through sudo command execution  
- Correlated multi-stage attack behavior using source IP, username, and command data 

## Outcome
This lab demonstrates foundational skills in security monitoring, log analysis, and threat detection, which are essential for SOC analyst and entry-level cybersecurity roles.

## What I Learned

- How to analyze authentication logs for security events
- How to use Splunk for log ingestion and SIEM-based analysis
- How to extract fields using regex for deeper investigation
- How to correlate events across multiple dimensions (IP, user, command)

## Detection Use Cases

- Brute-force detection based on failed login thresholds  
- Suspicious authentication behavior from single source IPs  
- Privilege escalation detection via sudo command monitoring  