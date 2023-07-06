# Revamping Cybersecurity with Azure: An Exploration into Honeynets and Security Operations Center (SOC)
![Cloud Honeynet / SOC](https://i.imgur.com/7s0rHfn.png)

## Overview

 This project showcases the orchestration of a compact honeynet within Microsoft Azure, luring real-time cyber threats from a global landscape. The primary aim is to exemplify ideal security protocols, response strategies to incidents, and the benefits of enhancing your cyber environment. We'll do this by deliberately deploying unprotected virtual machines visible to the public internet to bait potential hackers into our setup. The subsequent step involves funneling some log sources into the Log Analytics Workspace, after which Microsoft Sentinel will be used to build attack maps, raise alerts, and manage incidents. This process will be crucial in demonstrating the effects of hardening your cyber environment, based on the incidents recorded from a 24-hour surveillance period.

## Azure Components Employed

- Azure Virtual Network (VNet)
- Azure Network Security Group (NSG)
- Virtual Machines (2x Windows, 1x Linux)
- Log Analytics Workspace incorporating Kusto Query Language (KQL) Queries
- Azure Key Vault 
- Azure Storage Account 
- Microsoft Sentinel 
- Microsoft Defender for Cloud 


## Initial Architecture
![Architecture Diagram](https://i.imgur.com/c2E0AtK.png)

 - In the initial phase of the project, resources were configured to entice interaction from the public internet. Virtual Machines had their Network Security Groups (NSGs) and inbuilt firewalls set to allow unobstructed access from all sources. Additionally, other resources like storage accounts and databases were made publicly accessible, devoid of any Private Endpoints for augmented security. These machines were then left exposed to the public for a full day to generate the attack maps detailed below. 
 <br />
 
 <b>This attack map shows the number of incidents caused by leaving the Network Security Group (NSG) open. </b>
 
   ![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/bNOtiKt.png)<br>

 <br />
 <br />
 
 <b>This attack map demonstrates the incidents relating to syslog authentication failures on the Linux server. </b>
 
![Linux Syslog Auth Failures](https://i.imgur.com/nFR0Ehf.png)<br>

 <br />
 <br />
 
 <b>This attack map exhibits RDP and SMB failures on the Windows machine.</b>
 
![Windows RDP/SMB Auth Failures](https://i.imgur.com/4bylhdW.png)<br>

 <br />
 <br />
 
 <b>This attack map presents the failures encountered by the MSSQL server.</b>
 
![MSSQL](https://i.imgur.com/TYIlNVI.png)<br>

 <br />
 <br />
 
 ## Post-Security Enhancement Architecture

After documenting the incidents from the "Before" phase, the next step involved integrating robust security measures to improve the environment's resilience against cyber threats. The applied enhancements included:

- <b>Network Security Groups (NSGs)</b>: The NSGs were fortified by exclusively permitting traffic from my public IP address. All other traffic was blocked based on the newly set parameters.

- <b>Built-in Firewalls</b>: The firewalls within the virtual machines were configured to deny access to unauthorized users. 

- <b>Private Endpoints</b>: For additional Azure resources, public endpoints were replaced with Private Endpoints. This ensured the limited accessibility of sensitive resources, such as storage accounts and databases, to the virtual network alone.

## Attack Maps After Hardening / Security Controls

<br />

```After implementing the security measures, the map queries yielded no results, implying no instances of malicious activity during the 24-hour period post-hardening.```

 <br />
 
## Metrics Before and After Security Enhancements

Before and after the security improvements, metrics were recorded for comparison over a 24-hour period:<br/>
Before Hardening / Security Controls<br/>
Start Time 2023-07-04 12:45 AM<br/>
Stop Time 2023-07-05 12:45 AM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)            | 4358
| Syslog (Linux VM)                   | 2345
| SecurityAlert (Microsoft Defender for Cloud            | 6
| SecurityIncident (Sentinel Incidents)        | 73
| NSG Inbound Malicious Flows Allowed | 103

<br/>


After Hardening / Security Controls<br/>
Start Time 2023-07-05 4:15 PM<br/>
Stop Time	2023-07-06 4:15 PM


| Metric                   | Count
| ------------------------ | -----
| SecurityEvent (Windows VM)            | 2364
| Syslog (Linux VM)                   | 24
| SecurityAlert (Microsoft Defender for Cloud            | 0
| SecurityIncident (Sentinel Incidents)        | 0
| NSG Inbound Malicious Flows Allowed | 0

<br/>


## Implementation of NIST 800.61r2 Computer Incident Handling Guide

Every simulated attack was addressed following the recommendations of NIST SP 800-61 r2.

![NIST 800.61](https://i.imgur.com/6PTG7c0l.png)

Each organization will have policies related to an incident response that should be followed. This event is just a walkthrough for possible actions to take in the detection of malware on a workstation.  

#### Preparation

- The Azure lab was set up to ingest all of the logs into Log Analytics Workspace, Sentinel and Defender were configured, and alert rules were put in place.

#### Detection & Analysis

- Malware has been detected on a workstation with the potential to compromise the confidentiality, integrity, or availability of the system and data.
- Assigned alert to an owner, set the severity to "High", and the status to "Active"
- Identified the primary user account of the system and all systems affected.
- A full scan of the system was conducted using up-to-date antivirus software to identify the malware.
- Verified the authenticity of the alert as a "True Positive".
- Sent notifications to appropriate personnel as required by the organization's communication policies.

#### Containment, Eradication & Recovery

- The infected system and any additional systems infected by the malware were quarantined.
- If the malware was unable to be removed or the system sustained damage, the system would have been shut down and disconnected from the network.
- Depending on organizational policies the affected systems could be restored known clean state, such as a system image or a clean installation of the operating system and applications. Or an up-to-date anti-virus solution could be used to clean the systems. 

#### Post-Incident Activity

- In this simulated case, an employee had downloaded a game that contained malware. 
- All information was gathered and analyzed to determine the root cause, extent of damage, and effectiveness of the response. 
- Report disseminated to all stakeholders.
- Corrective actions are implemented to remediate the root cause.
- And a lessons-learned review of the incident was conducted.

<br />

## Conclusion

This project successfully designed a miniature honeynet within Microsoft Azure, integrating log sources into a Log Analytics workspace. Microsoft Sentinel was harnessed to generate alerts and manage incidents from the ingested logs. Metrics were assessed in the unsecure environment pre-security controls and post-implementation of these controls. The significant decline in security incidents post-enhancements underscores their effectiveness in protecting the environment.

However, it's essential to consider that with a higher utilization of network resources by regular users, there could have been an increase in security events and alerts within the 24-hour period post-security control implementation.
