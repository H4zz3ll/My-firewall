An open-source, AI-assisted firewall designed to detect, analyze, and prevent lateral movement through behavioral network analysis, traffic inspection, segmentation, and automated threat response.

Overview

Sentinel is an open-source next-generation firewall focused on one of the most critical stages of modern cyber attacks: lateral movement.

Instead of relying exclusively on static firewall rules, Sentinel continuously analyzes network traffic and communication patterns to identify behavior that may indicate reconnaissance, credential abuse, unauthorized service access, or attempts to move between systems inside a network.

The project combines traditional firewall capabilities with behavioral analysis and AI-assisted pattern recognition, allowing suspicious activity to be detected based on how devices communicate rather than solely on predefined signatures.

The ultimate goal is to create a firewall capable of understanding the normal behavior of a network, identifying deviations from that behavior, and taking appropriate defensive actions.

<img width="1335" height="827" alt="image" src="https://github.com/user-attachments/assets/6e7b3d3b-95d2-4511-b1f5-9b63f30f2d97" />

If an endpoint in the user network begins attempting unusual connections to multiple internal servers, Sentinel can analyze the behavior and determine whether the activity resembles reconnaissance or lateral movement.

Depending on the configured security policy, the firewall can then alert, restrict, isolate, or block the communication.

Key Features:
Network Segmentation

Designed to limit communication between network segments and reduce the attack surface.

Examples include:

User → Server restrictions
IoT → LAN isolation
Guest → Internal network isolation
Server → Server access control
Management network isolation
VLAN-based security policies

 Traffic Analysis

Sentinel analyzes network traffic to build a picture of how devices communicate.

Potentially relevant signals include:

Source and destination
Ports
Protocols
Connection frequency
Connection bursts
Repeated failed connections
Internal scanning behavior
Unusual communication paths
New device relationships
Changes in normal traffic patterns

The objective is not simply to ask:

"Is this IP address malicious?"

but also:

"Is this behavior normal for this device?"

 AI-Assisted Pattern Recognition

One of Sentinel's core concepts is behavioral analysis.

Instead of depending entirely on manually created signatures, the system can learn or model normal network behavior and identify significant deviations.

For example:

Normal behavior:

Workstation → DNS
Workstation → Web
Workstation → Printer

              ↓

Suspicious behavior:

Workstation
     │
     ├──► Server A : 445
     ├──► Server B : 445
     ├──► Server C : 445
     ├──► Server D : 445
     └──► Server E : 445

A sudden increase in SMB connections across multiple internal systems could become a behavioral signal requiring investigation.

The AI layer is intended to assist with:

Anomaly detection
Behavioral profiling
Traffic classification
Pattern recognition
Suspicious activity correlation
Risk assessment
Detection of previously unseen patterns

AI-generated decisions should remain explainable and auditable rather than functioning as an opaque "black box."

 Lateral Movement Detection

Sentinel is specifically designed to identify behaviors commonly associated with lateral movement.

Potential indicators include:

Internal network scanning
Abnormal port enumeration
Unexpected SMB activity
Unexpected RDP connections
SSH connection anomalies
Repeated authentication attempts
Unusual host-to-host communication
Sudden access to previously unused services
Abnormal connection frequency
Communication between normally isolated network segments

Detection does not automatically mean malicious activity. Legitimate administrative tools and services can produce similar patterns.

Therefore, Sentinel should combine multiple signals before taking an automated defensive action.

⚡ Automated Response

When a threat is detected, Sentinel can potentially respond according to predefined policies.

Example:

Traffic
   │
   ▼
Inspection
   │
   ▼
Behavior Analysis
   │
   ▼
Suspicious Pattern?
   │
 ┌─┴─────────┐
 │           │
 NO         YES
 │           │
 ▼           ▼
Allow     Risk Analysis
             │
        ┌────┴────┐
        │         │
      Alert     Block
        │         │
        └────┬────┘
             ▼
          Logging

Possible responses include:

Allow
Alert
Log
Rate-limit
Temporarily block
Isolate an endpoint
Block a specific connection
Quarantine a device
Require administrator approval

Automated blocking should be configurable to minimize false positives and prevent legitimate administrative activity from being interrupted.

 Explainable Detection

A major design goal is to make security decisions understandable.

Instead of simply displaying:

THREAT DETECTED

Sentinel could provide:

Suspicious Activity Detected

Source:
10.0.10.42

Destination:
10.0.20.0/24

Observed behavior:
• 37 hosts contacted
• 5 previously unused ports
• 23 SMB connections
• Activity increased 840% above baseline

Classification:
Potential lateral movement

Action:
Traffic blocked

Confidence:
92%

This makes the system useful not only for automated protection but also for security analysis and incident response.

📊 Security Dashboard

The project can provide a centralized dashboard for monitoring:

Active connections
Blocked connections
Suspicious hosts
Network segments
Detected anomalies
Security events
Traffic statistics
AI classifications
Historical activity
Threat timelines

Example:

┌──────────────────────────────────────────┐
│              SENTINEL                    │
├──────────────────────────────────────────┤
│ Network Status:          PROTECTED       │
│ Active Connections:      1,284           │
│ Blocked Connections:       37            │
│ Suspicious Hosts:           2            │
│ Critical Events:            0            │
├──────────────────────────────────────────┤
│ Recent Events                            │
│                                          │
│ [HIGH] Internal Scan      10.0.10.42     │
│ [MED]  Anomaly Detected   10.0.20.17     │
│ [LOW]  New Device         10.0.30.51     │
└──────────────────────────────────────────┘
 Security Philosophy

Sentinel follows several security principles:

Zero Trust

Network location alone should not imply trust.

Least Privilege

Devices should only communicate with the systems and services they actually require.

Defense in Depth

Firewall rules, segmentation, behavioral analysis, logging, and automated response should complement one another.

Assume Breach

The architecture should limit the damage caused by a compromised endpoint.

Explainability

Security decisions should provide enough context for administrators to understand why an event was detected or blocked.

 Proposed Architecture
                    ┌─────────────────┐
                    │     Internet    │
                    └────────┬────────┘
                             │
                     ┌───────▼───────┐
                     │  Packet Layer │
                     └───────┬───────┘
                             │
                     ┌───────▼───────┐
                     │ Traffic       │
                     │ Inspection    │
                     └───────┬───────┘
                             │
                ┌────────────▼────────────┐
                │ Behavioral Analysis     │
                └────────────┬────────────┘
                             │
                     ┌───────▼───────┐
                     │ Pattern        │
                     │ Recognition    │
                     └───────┬───────┘
                             │
                     ┌───────▼───────┐
                     │ Risk Engine    │
                     └───────┬───────┘
                             │
                ┌────────────▼────────────┐
                │ Policy / Response      │
                └────────────┬────────────┘
                             │
                ┌────────────▼────────────┐
                │ Allow / Alert / Block  │
                │ Isolate / Log          │
                └─────────────────────────┘

The architecture is intended to keep the packet-processing layer, detection engine, AI/ML components, and response engine modular.

This allows individual components to be replaced or improved without redesigning the entire firewall.

 Project Status

Early development / experimental

Sentinel is currently being developed as an open-source security research and engineering project.

Features may be incomplete, experimental, or subject to architectural changes.

Do not deploy experimental builds as the sole security control for production infrastructure.

 Long-Term Goals
 Stateful firewall
 VLAN-aware filtering
 Network segmentation
 Deep traffic analysis
 Behavioral baselines
 Anomaly detection
 AI-assisted classification
 Lateral movement detection
 Automated containment
 Endpoint isolation
 Security event dashboard
 Real-time alerts
 REST API
 Prometheus metrics
 Docker support
 Proxmox deployment
 High-availability support
 Detailed audit logging
 Explainable detection engine

Research & Development

Sentinel is also intended to be a platform for experimenting with modern defensive security techniques, including:

Network behavior analysis
Anomaly detection
Machine learning for cybersecurity
Network segmentation
Intrusion detection
Automated incident response
Threat correlation
Security telemetry
Zero-trust architectures

The project prioritizes defensive security and controlled testing environments.
