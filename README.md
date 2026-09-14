 CS-Shield: Wazuh Log Monitoring for SCADA Networks

 Overview

CS-Shield is a defensive monitoring framework built to secure SCADA (Supervisory Control and Data Acquisition) networks against cyber threats. Industrial Control Systems commonly rely on the Modbus/TCP protocol, which lacks built-in authentication or encryption, leaving them exposed to unauthorized access, malicious write operations, and network-based attacks such as scanning.

This project simulates a small-scale industrial environment (a PLC-controlled water tank system) and layers real-time traffic monitoring, intrusion detection, and centralized log analysis on top of it to detect and respond to these threats.

This repository documents the **Wazuh log monitoring and alerting component** of the project.

 My Role

I owned the Wazuh piece of the monitoring stack. My responsibilities included:

* Configuring Wazuh for centralized log collection from the SCADA/Modbus-TCP simulation environment
* Writing custom alert rules to flag suspicious activity — including unauthorized Modbus register writes and malformed packet injection
* Setting up and monitoring the Wazuh dashboard for real-time visualization of alerts and events
* Correlating log data to identify attack patterns during simulated attack scenarios (unauthorized writes, network scanning)

The broader CS-Shield project was a 5-person team effort. Teammates handled the PLC simulation (OpenPLC), process visualization (Node-RED), and network-level intrusion detection (Suricata, Zeek). This repo focuses specifically on the Wazuh log monitoring layer that I built.

 What I Configured

Log collection: Set up Wazuh agents/log sources to ingest events from the Ubuntu monitoring environment, including authentication logs, system events, and application logs relevant to the simulated attack surface
Alert rules: Defined detection rules to surface malicious Modbus write attempts and malformed traffic flagged upstream by Suricata
Dashboard: Configured the Wazuh dashboard to display real-time alert counts, authentication events, and MITRE ATT\&CK technique mapping for detected activity

See [`wazuh-config/`](./wazuh-config) for the rule and configuration files.

 Results

During attack simulation (unauthorized register writes via modpoll/mbpoll, malformed Modbus packet injection, and network scanning), the Wazuh monitoring setup successfully surfaced:

Real-time alerts correlated with MITRE ATT\&CK techniques
Authentication events, including PAM login activity and sudo-to-root escalations
AppArmor denial events
Rootcheck security alerts

See [`screenshots/`](./screenshots) for the dashboard views and detected event logs.

 Tools Used

Wazuh — centralized log collection, alert correlation, and security monitoring
Ubuntu Linux — deployment and monitoring environment

*(Other tools used elsewhere in the broader CS-Shield project — OpenPLC, Node-RED, Suricata, Zeek, Kali Linux — were owned by teammates and are not covered in this repo.)*

Repository Structure
cs-shield-wazuh-monitoring/
├── wazuh-config/    # Wazuh rules, decoders, and configuration snippets
├── screenshots/     # Dashboard views and detected event evidence
├── docs/            # Architecture notes
└── README.md


 Project Context

CS-Shield was completed as a major academic project for the B.Tech in Computer Science and Engineering (Cyber Security \& Cyber Defense specialization) at Sri Sri University, in collaboration with CyberDojo — The School of Cyberdefence.



