# OSSEC-HIDS
## Outline
### Network Intrusion
- Definition
- Intrusion detection system
### OSSEC
- Definition
- Purposes
- Stakeholders
- Benefits
- Real-world impact
### Technical 
- Installation
- Log Monitoring
- Integrity Checking

## What is network intrusion?
Any unauthorised action on a digital network is referred to as a network intrusion. Network intrusions frequently include the theft of valuable network resources and virtually always threaten network and/or data security.
## Intrusion Detection System(IDS)
An Intrusion Detection System (IDS) is a network traffic monitoring system that detects suspicious behaviour and sends out notifications when it is found. It's a software that searches a network or system for malicious activities or policy violations.
![image](https://user-images.githubusercontent.com/101413304/158044875-157579ba-2e24-40cf-a146-67c6e6178600.png)

### Detection Method of IDS
- Signatured-based Method: Signature-based intrusion detection systems can easily detect attacks with patterns (signatures) already present in the system, but it is much more difficult to detect new malware attacks with unknown patterns (signatures).
- Anomaly-based Method: As new malware is generated at a rapid rate, anomaly-based IDS was designed to identify unknown malware threats. Machine learning is used in anomaly-based IDS to construct a trustworthy activity model, and anything that comes in is compared to that model, and it is considered suspicious if it is not found in the model.

## What the OSSEC does?
OSSEC-HIDS is a host-based intrusion detection system that is free and open-source.

OSSEC offers four main features
- Log analysis 
  - The method used to detect attacks on a network, system, or application utilising logs as the primary source of information.  It can also be used to detect software misuse, policy violations, and other types of illegal behaviour
- Integrity checking
  - looking for changes in the checksums of the key files in the system and on the Windows registry
- Rootkit detection
  - Rootkit detection is performed on any systems where the agent is installed. To detect any possible rootkit installed, rootkit detection engine will be run every X minutes
- Active response
  - Active Response can run applications on an agent or server in response to specific alerts, alert levels, or rule groups and it also works for starting a syscheck scan or restarting OSSEC on a remote agent.

## How does OSSEC work?
OSSEC has a central manager which is in charge of monitoring and receiving data from agents, syslog, databases, and agentless devices. It stores the file integrity checking databases, the logs, events, and system auditing entries.

The agent will gather information and forward it to the manager for analysis and correlation.
![image](https://user-images.githubusercontent.com/101413304/158046271-3242a4a1-d0cc-4538-8743-e67b2ab5fbcd.png)
This diagram shows the central manager receiving events from the agents and system logs from remote devices. When certain conditions is detected, active responses can be performed and the administrator is notified.

## Who use OSSEC?
OSSEC is a multiplatform, open source and free host intrusion detection system, so it is a world's widely used tool. It is almost used by everyone from large or small companies.

## Why OSSEC would be useful?
- Compliance Requirements
- Multi platform
- Real-time and Configurable Alerts
- Integration with current infrastructure
- Centralized management
- Agent and agentless monitoring

## Real World Impact
- Support the allocation of security resources
- Examine the security countermeasures' efficiency
- Track virtual machines 
- Extend service options to a wider range of clients
- Centralized log reporting

## Supported Systems
- Operating Systems
  - GNU/Linux
  - Windows
  - Mac OS
- Devices supported via Syslog 
  - Cisco IOS routers
  - Juniper Netscreen
  - VMWare ESXi
- Devices and Operating Systems via Agentless 
  - Cisco IOS routers
  - Juniper Netscreen
  - All operating systems specified in the “operating systems” section

[Here is the detail information of Supported System](https://www.ossec.net/docs/docs/manual/supported-systems.html)

## OSSEC Installation (Ubuntu) and access web interface
[Instructions](https://hendgrow.com/ugs/HendGrow-OSSEC-OPEN-SOURCE-HIDS-WITH-WEB-USER-INTERFACE.pdf)
### Notes
1. Choose models
    - Local (Only monitor a single system)
    - Client/Server (The clients(agents) provide log messages to the server and the server generates and distributes the alerts. The server is the only place where rules and decoders are installed.)
    - Agentless (No agents)
2. Choose the installation path
3. Enable email notification
4. Enable system integrity check
5. Enable rootkit detection engine
6. Enable active response
7. Set web interface permissions
![image](https://user-images.githubusercontent.com/101413304/158048764-e2f27c0e-aaac-4a85-b7db-00bdb3e74769.png)
8. Restart Apache and launch Web User Interface
![image](https://user-images.githubusercontent.com/101413304/158048778-95d67c3d-8a5d-414a-ac18-1ee84ee62c08.png)
![image](https://user-images.githubusercontent.com/101413304/158048743-67670b0b-2ad4-4a62-a8b1-07ed31ff270b.png)

## Log monitoring/analysis





























