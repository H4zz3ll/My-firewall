An open-source, AI-assisted firewall designed to detect, analyze, and prevent lateral movement through behavioral network analysis, traffic inspection, segmentation, and automated threat response.

Overview

Sentinel is an open-source next-generation firewall focused on one of the most critical stages of modern cyber attacks: lateral movement.

Instead of relying exclusively on static firewall rules, Sentinel continuously analyzes network traffic and communication patterns to identify behavior that may indicate reconnaissance, credential abuse, unauthorized service access, or attempts to move between systems inside a network.

The project combines traditional firewall capabilities with behavioral analysis and AI-assisted pattern recognition, allowing suspicious activity to be detected based on how devices communicate rather than solely on predefined signatures.

The ultimate goal is to create a firewall capable of understanding the normal behavior of a network, identifying deviations from that behavior, and taking appropriate defensive actions.

<img width="1335" height="827" alt="image" src="https://github.com/user-attachments/assets/6e7b3d3b-95d2-4511-b1f5-9b63f30f2d97" />

# Sentinel - AI-Powered Open-Source Firewall

> An open-source, AI-assisted firewall designed to detect, analyze, and prevent lateral movement through behavioral network analysis, traffic inspection, network segmentation, and automated threat response.

## Overview

Sentinel is an open-source next-generation firewall focused on detecting and preventing lateral movement inside networks.

Traditional firewalls primarily rely on predefined rules such as IP addresses, ports, protocols, and network zones. Sentinel aims to complement these mechanisms with behavioral analysis and AI-assisted pattern recognition.

The system analyzes network activity to identify unusual communication patterns, suspicious connections, internal reconnaissance, and other behaviors that may indicate an attacker attempting to move through the network.

The main goal is to reduce the impact of compromised devices by detecting suspicious behavior and restricting unauthorized communication between systems.

## Key Features

### Network Segmentation

Sentinel is designed to control communication between different network segments and reduce unnecessary access.

Examples include:

- VLAN-based access control
- User network isolation
- Server network isolation
- IoT network isolation
- Guest network isolation
- Management network isolation
- Inter-VLAN traffic filtering

### Traffic Inspection

Sentinel analyzes network traffic and connection metadata to understand how devices communicate.

Potential signals include:

- Source and destination addresses
- Ports
- Protocols
- Connection frequency
- Connection patterns
- Failed connection attempts
- Internal scanning behavior
- New communication relationships
- Changes from established behavioral baselines

### AI-Assisted Pattern Recognition

One of Sentinel's main concepts is behavioral analysis.

Instead of relying exclusively on predefined signatures, Sentinel can analyze normal network behavior and identify significant deviations.

The AI layer is intended to assist with:

- Anomaly detection
- Behavioral profiling
- Traffic classification
- Pattern recognition
- Suspicious activity correlation
- Risk assessment
- Detection of previously unseen patterns

The AI system should remain explainable and auditable, allowing administrators to understand why an event was considered suspicious.

## Lateral Movement Detection

Sentinel focuses particularly on detecting behaviors that may indicate lateral movement.

Potential indicators include:

- Internal network scanning
- Abnormal port enumeration
- Unexpected SMB connections
- Unexpected RDP connections
- SSH connection anomalies
- Repeated authentication attempts
- Unusual host-to-host communication
- Sudden access to previously unused services
- Abnormal connection frequency
- Communication across normally isolated network segments

A single event should not automatically be considered malicious. Sentinel is designed to correlate multiple signals before making automated security decisions.

## Automated Threat Response

When suspicious activity is detected, Sentinel can apply configurable security policies.

Possible responses include:

- Allow the connection
- Log the event
- Generate an alert
- Rate-limit traffic
- Block a connection
- Temporarily block a host
- Isolate an endpoint
- Quarantine a device
- Require administrator approval

Automated responses should be configurable to reduce false positives and avoid disrupting legitimate network activity.

## Explainable Security Events

Sentinel aims to provide detailed information about why an event was detected.

Example:

```text
Suspicious Activity Detected

Source: 10.0.10.42
Destination: 10.0.20.0/24

Observed behavior:
- Multiple internal hosts contacted
- Multiple previously unused ports
- Increased SMB activity
- Significant deviation from normal behavior

Classification:
Potential lateral movement

Action:
Traffic blocked
