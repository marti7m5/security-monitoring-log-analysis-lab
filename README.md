# Security Monitoring & Log Analysis Lab

## Overview
This project demonstrates basic security monitoring and log analysis techniques using a simulated environment. The goal is to identify suspicious activity and understand how security events appear in system and network logs.

## Objectives
- Analyze system and network logs
- Identify failed login attempts and suspicious behavior
- Apply SIEM concepts such as event correlation and detection
- Understand indicators of compromise (IOCs)

## Tools Used
- Splunk (or log analysis tools)
- Linux (Ubuntu / Kali)
- Sample system and network logs

## Key Activities
- Ingested and reviewed log data
- Created queries to identify failed login attempts and abnormal activity
- Correlated events across logs to detect suspicious behavior
- Investigated potential security incidents based on log evidence

## Project Structure
- `/logs` – Sample log files used for analysis  
- `/queries` – Search queries used to detect events  
- `/screenshots` – Evidence of analysis and findings  

![Failed Login Analysis](screenshots/grep -n failed password auth log.png.png)

## Outcome
This lab demonstrates foundational skills in security monitoring, log analysis, and threat detection, which are essential for SOC analyst and entry-level cybersecurity roles.
