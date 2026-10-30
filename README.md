# NetworkWalks Cybersecurity Internship

A practical cybersecurity learning journey documenting hands-on laboratory setup, network configuration, packet analysis, and security investigation exercises as part of my internship with **NetworkWalks**.

This repository serves as a technical record of the tools, configurations, experiments, findings, and concepts explored throughout the internship.

---

## Overview

The internship focuses on developing practical cybersecurity skills through guided exercises and hands-on experimentation.

The current work is organised into two major areas:

1. **Cybersecurity Laboratory Setup:** Building and configuring a virtual cybersecurity laboratory using Kali Linux and Oracle VirtualBox.
2. **Wireshark SOC Labs:** Analysing network traffic, identifying suspicious communication patterns, and investigating TCP-based scanning activity.

## Projects

### 01. Main Project: Cybersecurity Lab Setup

**Objective:** Establish a functional Linux-based cybersecurity laboratory for practical security exercises.

**Environment:**
- Host operating system: macOS
- Hardware: Apple Silicon
- Virtualisation: Oracle VirtualBox
- Guest operating system: Kali Linux ARM64
- Network configuration: VirtualBox NAT Network

**Work undertaken:**
- Created and configured a Kali Linux virtual machine.
- Allocated virtual hardware resources, including CPU, memory, and storage.
- Configured a dedicated VirtualBox NAT Network.
- Worked on network addressing and interface configuration.
- Performed connectivity and internet access tests.
- Verified network configuration using Linux networking utilities.

**Tools and technologies:**
- Kali Linux
- Oracle VirtualBox
- Linux Terminal
- NetworkManager
- IP networking utilities

[View laboratory setup and screenshots](./01-MAIN-PROJECT-CYBERSECURITY-LAB-SETUP/)

---

### 02. Additional Project: Wireshark SOC Labs

**Objective:** Develop practical network traffic analysis skills through packet-level investigation.

#### Task 01: Identify the Attacker's IP

Investigated a network capture containing TCP connection attempts to identify the source of a port scanning activity.

**Investigation process:**

- Examined captured packets using Wireshark.
- Applied TCP SYN display filters to isolate connection initiation attempts.
- Examined source and destination IP addresses.
- Identified the attacker and target systems.
- Analysed TCP source and destination ports.
- Distinguished open-port and closed-port responses through TCP flags.
- Classified the observed activity as a TCP SYN port scan.

**Observed findings:**

| Parameter | Observation |
|---|---|
| Attacker IP | `192.168.10.66` |
| Target IP | `192.168.10.20` |
| Repeated source port | `52311` |
| Unique destination ports attempted | 40 |
| Closed-port responses counted | 37 |
| Attack classification | TCP SYN port scan |

**Important TCP behaviour examined:**

| Server response | Interpretation |
|---|---|
| SYN, ACK | Indicates an open TCP port |
| RST, ACK | Indicates a closed TCP port |
| No response | May indicate filtering or an unanswered request |

**Useful Wireshark display filters:**

Isolate SYN packets:

`tcp.flags.syn == 1`

Identify the attacker's SYN packets:

`ip.src == 192.168.10.66 && tcp.flags.syn == 1`

Identify SYN-ACK responses:

`ip.src == 192.168.10.20 && ip.dst == 192.168.10.66 && tcp.flags.syn == 1 && tcp.flags.ack == 1`

Identify RST-ACK responses:

`ip.src == 192.168.10.20 && ip.dst == 192.168.10.66 && tcp.flags.reset == 1 && tcp.flags.ack == 1`

The exact open-port list will be documented after cross-checking the SYN-ACK responses in the original capture.

[View Wireshark investigation and screenshots](./02-EXTRA-PROJECT-WIRESHARK-SOC-LABS/)

---

## Technical Skills Developed

### Operating Systems and Virtualisation
- Kali Linux
- Linux command-line operations
- Virtual machine configuration
- Virtual networking

### Networking
- TCP/IP fundamentals
- IP addressing and subnetting
- Network interfaces and routing
- TCP connection establishment
- TCP flags and port behaviour

### Network Security and Analysis
- Wireshark packet analysis
- Display filter construction
- TCP SYN scan identification
- Open and closed port analysis
- Network traffic investigation

### Development and Documentation
- Git and GitHub
- Markdown documentation
- Technical screenshots and evidence organisation

---

## Repository Structure

```text
NETWORKWALKS-INTERNSHIP/
│
├── README.md
│
├── 01-MAIN-PROJECT-CYBERSECURITY-LAB-SETUP/
│   ├── README.md
│   └── screenshots/
│
└── 02-EXTRA-PROJECT-WIRESHARK-SOC-LABS/
    ├── README.md
    │
    └── 01-IDENTIFY-THE-ATTACKERS-IP/
        ├── README.md
        └── screenshots/
```

Additional tasks, experiments, and documentation will be added as the internship progresses.

---

## Learning Approach

My focus throughout this internship is not merely on completing individual tasks, but on understanding the underlying concepts, interpreting real network behaviour, and developing the ability to investigate security-related problems independently.

Each exercise is documented with its objective, methodology, observations, and technical findings.

## Disclaimer

This repository is intended for educational and authorised cybersecurity training purposes.

All practical security exercises should be conducted only within controlled laboratory environments or systems for which explicit permission has been granted.

Sensitive information, credentials, and original packet captures containing potentially confidential traffic are intentionally excluded from version control.

---

**Repository:** [NetworkWalks Cybersecurity Internship](https://github.com/KChaitanyaaa/networkwalks-internship)
