# Building a SOC + Honeynet in Azure (Live Traffic)
![Image](https://github.com/users/kendalldollarton/projects/1/assets/159062074/b9a08bf6-9b57-411d-8fb9-3c0bfa06b4d2)

## Introduction

In this project, I constructed a miniature honeynet within Microsoft Azure.  This included consolodating log data from various resources into a Log Analytics workspace, which is then utilized by Microsoft Sentinel to build attack maps, trigger alerts, and generate incidents. I then proceeded to assess security metrics within the vulnerable environment for a duration of 24 hours. The metrics we will show are listed below.

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Image](https://github.com/users/kendalldollarton/projects/1/assets/159062074/036ea783-49de-413c-835d-726e906329c4)

## Architecture After Hardening / Security Controls
![Image](https://github.com/users/kendalldollarton/projects/1/assets/159062074/12963945-97de-4091-b093-e45e226668b4)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "**BEFORE**" metrics, all resources were initially deployed with exposure to the internet. The Virtual Machines operated with both their Network Security Groups and built-in firewalls configured to be wide open for easy access. All other resources were deployed with public endpoints visible to the internet. (No use for Private Endpoints)

For the "**AFTER**" metrics, Network Security Groups were hardened by blocking ALL traffic except my admin workstation.  All other resources benefited from enhanced protection through the utilization of their built-in firewalls and Private Endpoints.

## Attack Maps Before Hardening / Security Controls

![Image](https://github.com/users/kendalldollarton/projects/1/assets/159062074/c80ba133-36d5-425c-9e69-2944d72d0d5c)

![Image](https://github.com/users/kendalldollarton/projects/1/assets/159062074/c2548499-741c-46b2-9481-f4cf25546cbf)

![Image](https://github.com/users/kendalldollarton/projects/1/assets/159062074/73e05f50-54b4-426c-a6c5-c2bd169f981f)

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-02-17 17:04:11
Stop Time 2023-02-18 17:04:59

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 20194
| Syslog                   | 3881
| SecurityAlert            | 16
| SecurityIncident         | 367
| AzureNetworkAnalytics_CL | 915

## Attack Maps Before Hardening / Security Controls

```All map queries returned no results due to no instances of malicious activity occuring for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-02-18 18:03
Stop Time	2023-02-19 18:51

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 9108
| Syslog                   | 33
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

Within this project, a compact honeynet was established within Microsoft Azure, with log sources integrated into a Log Analytics workspace. Microsoft Sentinel was utilized to initiate alerts and generate incidents by using the ingested logs. Furthermore, security metrics were assessed in the vulnerable environment prior to the security controls being implemented and then reassessed after implementing security measures. It was observed that the implementation of security controls led to a significant reduction in both the number of security events and incidents.

## Languages Used:

- PowerShell: Extracted RDP failed login logs from Windows Event Viewer
- Structured Query Language (SQL)
- Kusto Query Language (KQL)

## Utilities Used:

- ipgeolocation.io: IP Address to Geolocation API

![Image](https://github.com/users/kendalldollarton/projects/1/assets/159062074/b9aaadaf-031d-4656-8483-0e5301e824e6)

Project Outline:

Josh Madakor is an information technology and cybersecurity professional, instructor, and influencer who deserves a well written appreciation note for creating this lab. I was able to follow a step by step tutorial through Josh's online cybersecurity course that he has created. Josh's purpose for creating this lab was to allow his students who do not have experience with these tools to develop a foundational understanding and gain experience. After following Josh's step by step instructions it was very informing to see the personal results that my SOC + honeynet was able to collect. I was able to understand how other countries are using RDP Brute Force daily to hack into any access point can find around the world. This lab has helped me gain foundational knowledge and experience with SIEM tools, SQL, KQL, Azure, Linux, Network protocols, Security controls, Geolocational data. I highly reccomend this lab to anyone that is looking to begin their career in IT or cybersecurity. 

Works Cited:

Madakor, Josh. “Siem Tutorial | Azure Sentinel Tutorial Map with Live Cyber Attacks!” YouTube, YouTube, 1 Nov. 2021, www.youtube.com/watch?v=RoZeVbbZ0o0.
