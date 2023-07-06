# Enhancing Cybersecurity with Azure: Real-Time Cyberattack Simulation and Analysis

## Project Overview

This project presents an Azure-powered honeynet simulation designed to attract and analyze real-time cyber threats from around the globe. The primary goal is to illustrate robust security strategies, effective incident response techniques, and the profound benefits of an enhanced cybersecurity posture. 

To achieve this, we have purposely set up vulnerable virtual machines exposed to the public internet, acting as bait for potential attackers. Following the integration of log sources into the Log Analytics Workspace, we utilize Microsoft Sentinel to generate attack maps, alerts, and incident reports. This approach allows us to measure the impact of security hardening based on incidents recorded during a 24-hour window.

## Azure Resources Deployed

- Azure Virtual Network (VNet)
- Azure Network Security Group (NSG)
- Virtual Machines (2x Windows, 1x Linux)
- Log Analytics Workspace with Kusto Query Language (KQL) Queries
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel
- Microsoft Defender for Cloud

## Pre-Hardening Architecture

During the initial phase, we deployed all resources with the intent of attracting public internet traffic. The Virtual Machines, with both their Network Security Groups (NSGs) and built-in firewalls open, provided unrestricted access from any source. Concurrently, other resources such as storage accounts and databases were set up with public endpoints, neglecting Private Endpoints for enhanced security. These resources were exposed to the public for a day, generating the subsequent attack maps.

Attack maps include:

- NSG Allowed Inbound Malicious Flows ![image](https://github.com/Kermini/Azure-Honeynet/assets/138714889/94610c0b-e1d1-4a50-87a1-3d0490438a0d)

- Linux Syslog Authentication Failures ![image](https://github.com/Kermini/Azure-Honeynet/assets/138714889/7dc328c2-4059-4d02-bb68-aa85dea7af00)

- Windows RDP/SMB Authentication Failures ![image](https://github.com/Kermini/Azure-Honeynet/assets/138714889/5a6f7062-4c39-4e58-84d6-f425e2a84b4d)

- MSSQL Server Failures ![image](https://github.com/Kermini/Azure-Honeynet/assets/138714889/d604f864-ef80-4229-840d-e13e76e85b25)


## Post-Hardening Architecture

After analyzing incidents from the "Before" phase, we implemented rigorous security measures to bolster the environment's resilience against cyber threats. These improvements encompass:

- NSGs: We strengthened the NSGs by allowing only traffic from my public IP address.
- Built-in Firewalls: We configured the built-in firewalls on our virtual machines to deny access to unauthorized users.
- Private Endpoints: We substituted the public endpoints of our Azure resources with Private Endpoints, restricting the accessibility of sensitive resources to the virtual network.

Following the implementation of these measures, no malicious activity was detected during the subsequent 24-hour monitoring period.

## Metrics Analysis

We gathered and compared metrics from both the insecure and secure environment over a 24-hour period.

## Incident Handling Using NIST 800.61r2 Guidelines

For each simulated attack, we executed incident responses in alignment with the NIST SP 800-61 r2 guide.

![image](https://github.com/Kermini/Azure-Honeynet/assets/138714889/b57ac0b3-330c-49c6-a823-4520953b1464)


## Conclusion

Through this project, we demonstrated how a honeynet, constructed within Microsoft Azure, could effectively track and analyze real-world cyber threats. Utilizing Microsoft Sentinel, we were able to create alerts and manage incidents based on the analyzed log data. The comparison of metrics before and after the implementation of security controls showcased their crucial role in maintaining a secure environment.

It is important to note that with more frequent usage of the network resources, the number of security events and alerts within the 24-hour period post-implementation of security controls could potentially increase.
