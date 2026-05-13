# Enterprise Network Segmentation & Firewall Enforcement Lab

## Overview

This project demonstrates the deployment, validation, and remediation of an enterprise-style segmented network using Cisco infrastructure and a Palo Alto Networks firewall. The lab was intentionally deployed in an insecure state to simulate lateral movement vulnerabilities before implementing proper segmentation controls and firewall enforcement.

The environment includes VLAN segmentation, inter-VLAN routing, Palo Alto security zones, NAT, traffic monitoring, SPAN/Wireshark analysis, and security policy remediation.

---

# Objectives

* Build a segmented enterprise network
* Configure inter-VLAN routing through a Palo Alto firewall
* Simulate unrestricted lateral movement
* Capture insecure traffic flows using Wireshark
* Implement zone-based segmentation policies
* Restrict unauthorized access to sensitive server infrastructure
* Validate remediation using firewall traffic logs

---

# Technologies Used

## Networking

* Cisco IOS
* VLANs
* 802.1Q Trunking
* Static Routing
* OSPF
* SPAN Port Monitoring

## Security

* Palo Alto Networks Firewall
* Security Zones
* Inter-Zone Policies
* NAT Policies
* Traffic Monitoring

## Analysis

* Wireshark
* ICMP Testing
* Traffic Log Validation

---

# Network Topology

```text
                           AT&T ISP
                               |
                              R1
                               |
                       Palo Alto Firewall
                               |
                              SW1
                          Core Switch
                       /             \
                    SW2             SW3
                VLAN 10/30      VLAN 20/40
                 |      |         |      |
               PC1     R2      Server    R3
```

---

# VLAN Architecture

| VLAN | Purpose         | Subnet       |
| ---- | --------------- | ------------ |
| 10   | Corporate Users | 10.0.10.0/24 |
| 20   | Shared Servers  | 10.0.20.0/24 |
| 30   | Finance         | 10.0.30.0/24 |
| 40   | Engineering     | 10.0.40.0/24 |

---

# Firewall Segmentation Model

| Source            | Destination | Action |
| ----------------- | ----------- | ------ |
| VLAN 10           | VLAN 20     | Deny   |
| VLAN 30           | VLAN 20     | Deny   |
| VLAN 40           | VLAN 20     | Allow  |
| VLAN 10 ↔ VLAN 30 | Allow       |        |
| VLAN 10 ↔ VLAN 40 | Allow       |        |
| VLAN 30 ↔ VLAN 40 | Allow       |        |
| Internal VLANs    | Internet    | Allow  |

---

# Security Improvements

## Before Remediation

* Flat internal trust model
* Unrestricted lateral movement
* Broad allow-all firewall policies
* Exposed server infrastructure

## After Remediation

* Protected server enclave
* Controlled east-west traffic
* Zone-based policy enforcement
* Explicit allow/deny security policies
* Validated segmentation controls

---

# Wireshark & SPAN Analysis

Traffic was captured using a SPAN port configured on the core switch to monitor traffic between the Palo Alto firewall and SW1. Packet captures validated:

* Inter-VLAN traffic
* Lateral movement attempts
* VLAN tagging
* Allowed vs denied traffic flows
* Segmentation enforcement

---

# Validation Testing

## Successful Tests

* VLAN 10 ↔ VLAN 30
* VLAN 10 ↔ VLAN 40
* VLAN 30 ↔ VLAN 40
* VLAN 40 → VLAN 20
* Internet access from all VLANs

## Denied Tests

* VLAN 10 → VLAN 20
* VLAN 30 → VLAN 20

---

# Key Security Concepts Demonstrated

* Enterprise network segmentation
* East-west traffic filtering
* Least privilege access control
* Firewall policy remediation
* Lateral movement reduction
* Secure zone architecture
* Network traffic visibility

---

# Repository Structure

```text
/network-segmentation-lab
│
├── README.md
├── /images
├── /configs
├── /captures
```

---

# Screenshots Included

* VLAN configuration
* Trunk interfaces
* Palo Alto security zones
* Firewall policies
* NAT policies
* Traffic logs
* Wireshark captures
* Connectivity validation

---

# Final Outcome

This project successfully demonstrated the transition from a flat enterprise network to a segmented security architecture using Palo Alto firewall policy enforcement and Cisco switching infrastructure. The final design preserved legitimate business communication while restricting unauthorized access to protected server resources.
