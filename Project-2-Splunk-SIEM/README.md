Splunk SIEM — Windows Security Monitoring

Overview

This project was built to practice using Splunk as a SIEM in a Windows environment.

I used a Windows Server 2022 Domain Controller and Splunk Enterprise running on my host machine. The Windows Server sends Security Event Logs to Splunk through the Splunk Universal Forwarder.

The main focus was authentication monitoring, SPL searches, event investigation, and building a basic SOC dashboard.

Environment

Component: Windows Server 2022 (DC01 / NKAD)
Purpose: Generates Windows Security Events

Component: Splunk Universal Forwarder
Purpose: Collects and forwards logs

Component: Splunk Enterprise
Purpose: SIEM and log analysis

Component: VMware Workstation
Purpose: Virtual lab environment

Component: TCP 9997
Purpose: Splunk receiving port

Log Collection

The Universal Forwarder was configured to collect the Windows Security Event Log.

[WinEventLog://Security]
disabled = 0
index = main
start_from = oldest
current_only = 0
checkpointInterval = 5

Splunk Enterprise successfully received the Windows Security events.

SPL & Event Investigation

Successful Logons — Event ID 4624

index=main host=NKAD EventCode=4624

Used to identify successful authentication activity.

Failed Logons — Event ID 4625

index=main host=NKAD sourcetype="WinEventLog:Security" EventCode=4625

During testing, I generated failed authentication attempts and investigated the resulting events.

The events showed:

Account: Shadow
Source IP: 127.0.0.1
Logon Type: 2
Failure Reason: Unknown user name or bad password

The source address indicated that the activity came from the local machine, so the events were treated as lab-generated test activity rather than a remote attack.

Privileged Activity — Event ID 4672

index=main host=NKAD sourcetype="WinEventLog:Security" EventCode=4672
| stats count by Account_Name
| sort - count

Results included:

SYSTEM: 2,139
Shadow: 138

This was used to practice identifying privileged account activity.


Splunk Dashboard

Created a dashboard called Splunk SOC Monitoring.


The dashboard contains:

Failed Logons by Account and Source IP
Authentication Success vs Failure
Privileged Account Activity
Windows Security Events by EventCode


What I Practiced

Splunk SIEM fundamentals
SPL searching and filtering
Windows Security Event Logs
Authentication monitoring
Failed-logon investigation
Source IP investigation
Privileged activity monitoring
Basic SOC dashboard creation
Security event analysis 
