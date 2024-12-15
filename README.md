# Building a SOC + Honeynet in Azure (Live Traffic)
![image](https://github.com/user-attachments/assets/d4c3abc2-e269-45da-a1c8-b410180cd6b1)




![Cloud Honeynet + SOC porrtfolio leveld diagram](https://github.com/user-attachments/assets/6135ddc1-3d68-4025-b6db-b3f29b49cf24)




## Introduction

In this project, I created a small, controlled computer network in Microsoft's Azure cloud service. This network, called a "honeynet," helps us understand how attackers might try to break into our systems.
I collected logs from different parts of this network and stored them in a central location called the Log Analytics workspace. This information was then used by a security tool called Microsoft Sentinel to build visual maps of potential attacks, set off warnings when something suspicious happened, and create records of any incidents.

I measured several security metrics in the insecure environment over a 24-hour period. After applying security controls to harden the environment, I measured the metrics again for another 24 hours. The results of these measurements are shown below. 
The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![image](https://github.com/user-attachments/assets/6b5aa61d-1597-4924-aa1a-0c51610d9884)


## Architecture After Hardening / Security Controls
![Slide 3 for Get hUb Portfolio  After Hardenng](https://github.com/user-attachments/assets/7a0fde40-9e6a-4d0c-8ea8-68f7102ef5fd)


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

In the "BEFORE" setup, all resources were connected to the internet and easily visible to everyone. The computers' security settings and firewalls were set to allow all traffic, making them more vulnerable. Other resources were also visible to the internet because they didn't use private connections.

In the "AFTER" setup, network security was improved by blocking all traffic except for my admin workstation. Other resources were also better protected using stronger firewalls and private Endpoint.

## Attack Maps Before Hardening / Security Controls
![image](https://github.com/user-attachments/assets/86ca3519-6c4c-4d0e-a8e8-93d617883a76)
![image](https://github.com/user-attachments/assets/2858cd2c-1955-4862-b2e9-2581814909c4)
![image](https://github.com/user-attachments/assets/6748da3d-7ef9-4ced-8e75-f701a2610e68)



## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-03-15 17:04:29
Stop Time 2023-03-16 17:04:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 33636
| Syslog                   | 12721
| SecurityAlert            | 43
| SecurityIncident         | 462

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 9513
| Syslog                   | 67
| SecurityAlert            | 0
| SecurityIncident         | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
