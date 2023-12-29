# Building a SOC + Honeynet in Azure (Live Traffic)
![azureHoneynetImage](https://github.com/k-mcgeary/Azure-Project/assets/129139672/a476d110-7e9d-4fc5-af49-332818c61c0f)

## Introduction

In this project, I constructed a mini honeynet in Azure, integrated log sources into a Log Analytics workspace, utilized Microsoft Sentinel for attack mapping, alert triggering, and incident creation, measured security metrics in the insecure environment for 24 hours, implemented security controls to fortify the environment, and measured metrics for another 24 hours, presenting the results below:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://github.com/k-mcgeary/Azure-Project/assets/129139672/f0b45727-be75-48cc-8265-26f5020c0fa0)


## Architecture After Hardening / Security Controls
![Architecture Diagram](https://github.com/k-mcgeary/Azure-Project/assets/129139672/3d4b1182-77d8-40ab-9ff3-6d8ec519e167)


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (1 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoints.

## Attack Maps Before Hardening / Security Controls
![insecureNSGMap](https://github.com/k-mcgeary/Azure-Project/assets/129139672/ae4b9ca1-06ec-490a-b6b9-8a3ef60e1f6a)<br>
![insecureLinuxMap](https://github.com/k-mcgeary/Azure-Project/assets/129139672/89f08251-0700-498f-8d70-30e88c4bcf75)<br>
![insecureWindowsMap](https://github.com/k-mcgeary/Azure-Project/assets/129139672/c4c733a7-f109-45fd-a573-6503ebcb0580)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:<br>
Start Time 2023-12-26 09:30:00<br>
Stop Time 2023-12-27 09:30:00

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 25852
| Syslog                   | 7339
| SecurityAlert            | 283
| SecurityIncident         | 281
| AzureNetworkAnalytics_CL | 67796

## Supporting Log Snapshots
![insecureSecurityEvent](https://github.com/k-mcgeary/Azure-Project/assets/129139672/4c895c35-de61-49ce-9993-d1010c58a4d2)<br>
![insecureSyslog](https://github.com/k-mcgeary/Azure-Project/assets/129139672/7eff0c34-749f-4c5f-8a52-ddd7f96c02c0)<br>
![insecureWindowsDefender](https://github.com/k-mcgeary/Azure-Project/assets/129139672/30ca52e7-3dc2-439b-8788-f2c836bdc2e0)<br>
![insecureSentinelIncidents](https://github.com/k-mcgeary/Azure-Project/assets/129139672/8b262604-bac5-46af-92b8-3c53db4701c5)<br>
![insecureNSGRules](https://github.com/k-mcgeary/Azure-Project/assets/129139672/35a7134d-54a6-4ff0-bb53-87e8188da3da)<br>

## Attack Maps After Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:<br>
Start Time 2023-12-27 12:00:00<br>
Stop Time	2023-12-28 12:00:00

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 7651
| Syslog                   | 5
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Supporting Log Snapshots
![secureSecurityEvent](https://github.com/k-mcgeary/Azure-Project/assets/129139672/b4d852f2-bf28-4bb6-8d9b-9a0fc7c53db2)<br>
![secureSyslog](https://github.com/k-mcgeary/Azure-Project/assets/129139672/eb171143-78ef-40b2-ab4c-8a24d8b51355)<br>
![secureWindowsDefender](https://github.com/k-mcgeary/Azure-Project/assets/129139672/7005340f-d54e-43fd-a3b3-f8e9214990d6)<br>
![secureSentinelIncidents](https://github.com/k-mcgeary/Azure-Project/assets/129139672/66827ed9-74da-4679-8993-97bb27e17e31)<br>
![secureNSGRules](https://github.com/k-mcgeary/Azure-Project/assets/129139672/a319e3ac-e6eb-4bd4-9d72-93c1731f4694)<br>

## Conclusion

A mini honeynet was set up in Microsoft Azure with log sources integrated into a Log Analytics workspace, utilizing Microsoft Sentinel to trigger alerts and incidents based on ingested logs. After measuring metrics in the insecure environment both before and after implementing security controls, the significant reduction in security events and incidents underscored the effectiveness of the measures. It's worth considering that higher resource utilization by regular users could potentially lead to more security events and alerts within the 24-hour period following the security controls' implementation.
