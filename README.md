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
Any unauthorised action on a digital network is referred to as a network intrusion. Network intrusions frequently include the theft of valuable network resources and always threaten network and/or data security.

## Intrusion Detection System(IDS)
An Intrusion Detection System (IDS) is a network traffic monitoring system that detects suspicious behaviour and sends out notifications when it is found. It's a software that searches a network or system for malicious activities or policy violations.
![image](https://user-images.githubusercontent.com/101413304/158044875-157579ba-2e24-40cf-a146-67c6e6178600.png)

### Detection Method of IDS
- Signature-based Method: Signature-based intrusion detection systems can easily detect attacks with patterns (signatures) already present in the system, but it is much more difficult to detect new malware attacks with unknown patterns (signatures).
- Anomaly-based Method: As new malware is generated at a rapid rate, anomaly-based IDS was designed to identify unknown malware threats. Machine learning is used in anomaly-based IDS to construct a trustworthy activity model, and anything that comes in is compared to that model, and it is considered suspicious if it is not found in the model.

## What the OSSEC does?
OSSEC-HIDS is a host-based intrusion detection system that is free and open-source.

OSSEC offers four main features
- Log analysis 
  - The method is used to detect attacks on a network, system, or application utilising logs as the primary source of information.  It can also be used to detect software misuse, policy violations, and other types of illegal behaviour
- Integrity checking
  - looking for changes in the checksums of the key files in the system and on the Windows registry
- Rootkit detection
  - Rootkit detection is performed on any systems where the agent is installed. To detect any possible rootkit installed, rootkit detection engine will be run every X minutes
- Active response
  - Active Response can run applications on an agent or server in response to specific alerts, alert levels, or rule groups and it also works for starting a syscheck scan or restarting OSSEC on a remote agent.

## How does OSSEC work?
OSSEC has a central manager which is in charge of monitoring and receiving data from agents, syslog, databases, and agentless devices. It stores the file integrity checking databases, the logs, events, and system auditing entries.

The agents will gather information and forward it to the manager for analysis and correlation.
![image](https://user-images.githubusercontent.com/101413304/158046271-3242a4a1-d0cc-4538-8743-e67b2ab5fbcd.png)
This diagram shows the central manager receiving events from the agents and system logs from remote devices. When certain conditions are detected, active responses can be performed and the administrator is notified.

## Who use OSSEC?
OSSEC is a multiplatform, open source and free host intrusion detection system, so it is a world's widely used tool. It is almost used by everyone from large or small companies, as well as the individuals who need to detect network intrusion.

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
Log Analysis is performed inside OSSEC by the logcollector and analysisd processes. The first one gathers the events, while the second one analyzes them. It is done in real time.
![image](https://user-images.githubusercontent.com/101413304/158052006-073fb7ef-824a-4f51-b546-7c32f47c26e4.png)

For the log analysis flow of both local and agent/server architectures:
- Log collecting is performed by ossec-logcollector
- Analysis and decoding are performed by ossec-analysisd
- Alerting is performed by ossec-maild
- Active responses are performed by ossec-execd

Log flow inside analysisd has three main parts:
- Pre-decoding (extract known informations)
- Decoding (use user-defined decoder)
- Signatures (use user-defined rules)
![image](https://user-images.githubusercontent.com/101413304/158052164-b76d4bcf-70fd-4f58-b41f-fd6119461037.png)

### Testing using ossec-logtest
The ossec-logtest is installed into ```/var/ossec/bin```.
![image](https://user-images.githubusercontent.com/101413304/158052192-5402d28d-3daa-4d64-a42b-748a4ab52edf.png)

Phase 1 “pre-decodes” some information. The hostname is the system that produced the log message, program_name is the name of the application that generated the log, and log represents the rest of the log message.

Phase 2 identifies the log message as coming from decoder 'sshd'.

Phase 3 checks the rule, and it shows the rule id and the level of the rule.

### OSSEC Rules
- Stored as XML files
- Classification: from the lowest level (00) to the maximum level 16

[OSSEC Rules Classification and Group](https://www.ossec.net/docs/docs/manual/rules-decoders/rule-levels.html)

## Integrity checking (Syscheck)
The agent scans the system and send all the checksums to the server. The server stores the checksums and monitors them for changes. If something changes, an alert will then be sent.

The figure below is the main configure file on manager which contains the global setting and syscheck files. The global displays that the email notification is activated and it will send alert to the email we set before as long as the OSSEC reaches the alert level. For syscheck, the ```check_all``` option checks md5, sha1, owner, and permissions of the file. The ```ignore``` option (or `registry_ignore` for Windows registry entries) can be used to ignore files and folders.

![image](https://user-images.githubusercontent.com/101413304/158052204-f42d773c-7f7d-41e4-895e-703fc2b2b0d2.png)

OSSEC looks for the changes in the integrity of the system and sends the integrity checksum changed alerts to the website as the figure shows below.

![image](https://user-images.githubusercontent.com/101413304/158052205-c0c27d5f-224d-4c79-b0ad-7a7b00be974c.png)














