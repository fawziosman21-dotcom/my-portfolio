
Project 3 — Active Directory & Windows Security Lab

I built a small Windows domain environment using VMware with a Windows Server 2022 domain controller and a Windows 11 workstation.

LAB SETUP

DC01 — Windows Server 2022
CLIENT01 — Windows 11
Domain — lab.local
Network — VMware NAT
DC01 IP — 192.168.136.131

WHAT I DID

Active Directory

Installed Active Directory Domain Services and created the lab.local domain.

Created these OUs:

Admins
Workstations
Servers
Security Groups

CLIENT01 was moved into the Workstations OU.

Created the following domain account and groups:

User: doon.admin
Groups: Employees, IT-Admins

DNS AND DOMAIN JOIN

Configured CLIENT01 to use DC01 as its DNS server.

Tested DNS from CLIENT01 using:

nslookup lab.local

The domain resolved to:

192.168.136.131

CLIENT01 was then joined to the lab.local domain.

GROUP POLICY

Created a GPO called:

Workstation Security Baseline

The GPO was linked to the Workstations OU.

Configured password, account lockout, security auditing, and workstation security settings.

Verified the policy from CLIENT01 using:

gpresult /scope computer /r

The output showed:

Workstation Security Baseline
Default Domain Policy

as applied policies.

SECURITY AUDITING

Configured Advanced Audit Policy for:

Credential Validation
Kerberos Authentication Service
Logon
Logoff
Account Lockout
User Account Management
Security Group Management
Audit Policy Change

Checked the configuration using:

auditpol /get /category:*

Also checked the Windows Security log using Event Viewer.

Event ID 4634 was recorded for LAB\doon.admin.

WINDOWS FIREWALL

Checked Windows Defender Firewall on CLIENT01.

The Domain Profile was enabled.

Inbound connections were blocked by default and outbound connections were allowed by default.

Firewall settings were also controlled through Group Policy.

ENDPOINT HARDENING

The local Guest account was disabled on CLIENT01.

TROUBLESHOOTING

The first attempt to join CLIENT01 to the domain failed because the credentials entered were incorrect.

After correcting the credentials, CLIENT01 successfully joined lab.local.

EVIDENCE

The screenshots in this project are from my actual lab.

The full evidence report is available here:

[Project 3 Evidence Report](./PROJECT3_AD_SECURITY_EVIDENCE_REPORT_2026.pdf)

RESULT

The lab was completed successfully.

CLIENT01 is joined to the lab.local domain, located in the Workstations OU, receiving the workstation security GPO, generating security audit events, and using the configured Windows Firewall and endpoint security settings.
