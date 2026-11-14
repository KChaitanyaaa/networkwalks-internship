# WEEK 2 INTERNSHIP REPORT
## Cybersecurity and Ethical Hacking

**Student:** N. Krishna Chaitanya Narasagari  
**Programme:** B.Tech, Computer Science and Engineering (AI & ML)  
**Institution:** Central University of Karnataka  
**Internship Week:** Week 2  
**Environment:** Kali Linux running in VirtualBox  
**Reporting Period:** November 2026

# ABSTRACT

This report documents the practical work undertaken during Week 2 of the Cybersecurity and Ethical Hacking internship. The work focused on two selected project modules: footprinting and reconnaissance using multiple Kali Linux tools (W2-PM1), and network scanning using Zenmap (W2-PM5).

The first module involved examining publicly available domain information and identifying web technologies, DNS records, HTTP response headers and web application firewall characteristics. Six tools were used: WHOIS, WhatWeb, Nslookup, cURL, WAFW00F and DNSRecon.

The second module involved configuring a Kali Linux virtual machine, identifying its network configuration and performing host discovery using Zenmap and Nmap. A single-host discovery experiment and a subsequent subnet-wide Ping Scan were conducted within the VirtualBox NAT Network.

The experiments provided practical exposure to reconnaissance techniques, DNS enumeration, web technology fingerprinting and network host discovery. The limitations of virtualized network scanning and the interpretation of automated tool results are also discussed.

# CHAPTER 1: INTRODUCTION

## 1.1 Background

Cybersecurity involves protecting computer systems, networks and digital information against unauthorized access and malicious activities.

Reconnaissance and network discovery are important preliminary activities in security assessments. They help security professionals understand the publicly observable characteristics of a target and identify active hosts within an authorized network.

This week's internship activities focused on developing practical familiarity with reconnaissance tools and network scanning techniques using Kali Linux.

## 1.2 Objectives

1. Understand the fundamentals of footprinting and reconnaissance.
2. Examine publicly available domain registration information.
3. Identify web technologies and server characteristics.
4. Examine DNS records and HTTP response headers.
5. Identify web application firewall technologies.
6. Understand network addressing and subnet configurations.
7. Discover active hosts using Zenmap.
8. Interpret scan results and document network observations.

## 1.3 Experimental Environment

| Component | Configuration |
|---|---|
| Operating System | Kali Linux |
| Virtualization | VirtualBox |
| Network Mode | NAT Network |
| Interface | eth0 |
| Local IPv4 | 10.0.0.2 |
| Subnet | 10.0.0.0/24 |
| Default Gateway | 10.0.0.1 |
| Reconnaissance Tools | Kali Linux utilities |
| Network Scanner | Zenmap 7.991 / Nmap |

# CHAPTER 2: PM1 – FOOTPRINTING AND RECONNAISSANCE USING KALI LINUX TOOLS

## 2.1 Introduction

Footprinting is the process of collecting information about a domain or organization through publicly available information and observable network responses.

The practical exercise used six Kali Linux tools to examine the domain networkwalks.com. The objective was to understand the different types of information each tool can reveal.

## 2.2 Experiment 1: WHOIS

**Objective:** Examine domain registration information.

**Command:**
```bash
whois networkwalks.com
```

**Observations:**

The WHOIS query returned domain registration information, including registrar information, registration and domain status, nameserver information, registrant privacy protection, and technical and administrative contact details where available.

The registrant information showed privacy protection through Domains By Proxy, LLC.

**Result:** WHOIS demonstrated how domain registration databases can provide information about domain ownership, registrar services and domain status.

## 2.3 Experiment 2: WhatWeb

**Objective:** Identify web technologies used by the target website.

**Command:**
```bash
whatweb networkwalks.com
```

**Observations:**

| Component | Detection |
|---|---|
| Web server | Apache |
| CMS | WordPress 7.1.4 |
| JavaScript library | jQuery 3.7.1 |
| Frontend framework | Bootstrap 7.1.4 |
| Website title | Networkwalks Academy |
| Country identification | United States |
| IP address | 192.232.216.135 |

The website also exposed HTTP-related technologies and security headers.

**Result:** WhatWeb demonstrated how web application technologies can be identified through observable responses.

## 2.4 Experiment 3: Nslookup

**Objective:** Resolve the domain name and examine DNS information.

**Command:**
```bash
nslookup networkwalks.com
```

The exercise demonstrated the relationship between domain names and IP addresses through DNS resolution.

**Result:** DNS lookup provided a method of examining domain resolution and identifying associated DNS infrastructure.

## 2.5 Experiment 4: cURL

**Objective:** Examine HTTP response headers.

**Command:**
```bash
curl -I https://networkwalks.com
```

**Observations:**

| Header | Observed information |
|---|---|
| HTTP status | 200 OK |
| Server | Apache |
| Content-Type | text/html; charset=UTF-8 |
| Referrer-Policy | no-referrer-when-downgrade |
| X-Endurance-Cache-Level | 0 |
| X-nginx-cache | WordPress |

The response also contained a WordPress REST API link and cookie-related information.

**Result:** cURL demonstrated how HTTP response headers can provide information about server configuration and application behaviour.

## 2.6 Experiment 5: WAFW00F

**Objective:** Identify the Web Application Firewall protecting a website.

**Command:**
```bash
wafw00f networkwalks.com
```

**Observations:**

WAFW00F identified **ModSecurity (SpiderLabs)**. The tool reported that the website was behind a ModSecurity Web Application Firewall.

A comparison was also performed using ChatGPT's public domain:
```bash
wafw00f chatgpt.com
```

This returned a Cloudflare WAF identification. The comparison demonstrated that different websites can employ different firewall technologies.

**Result:** WAFW00F provided practical exposure to automated firewall fingerprinting. The exercise involved identification only, not bypassing or exploiting the firewall.

## 2.7 Experiment 6: DNSRecon

**Objective:** Enumerate publicly observable DNS records.

**Command:**
```bash
dnsrecon -d networkwalks.com
```

**Observations:**

| Record | Observation |
|---|---|
| SOA | ns6135.hostgator.com |
| NS | ns6135.hostgator.com |
| NS | ns6136.hostgator.com |
| A | 192.232.216.135 |
| MX | mail.networkwalks.com |
| TXT | SPF information |
| TXT | Google site verification |
| SRV | cPanel autodiscovery services |

The tool also reported that the DNSSEC query received no answer and flagged recursive DNS availability on the reported nameservers. A total of eight records were reported by the tool.

**Result:** DNSRecon demonstrated how DNS enumeration can reveal domain infrastructure, mail configuration and associated services.

## 2.8 PM1 Summary

| Tool | Primary purpose | Result |
|---|---|---|
| WHOIS | Domain registration | Registration details obtained |
| WhatWeb | Technology fingerprinting | Apache and WordPress identified |
| Nslookup | DNS resolution | Domain resolution examined |
| cURL | HTTP headers | HTTP response examined |
| WAFW00F | Firewall identification | ModSecurity identified |
| DNSRecon | DNS enumeration | Eight records reported |

## 2.9 Discussion

The six tools provided complementary perspectives on the target domain. WHOIS revealed registration-related information, while WhatWeb identified the web technologies. Nslookup and DNSRecon provided DNS-related observations. cURL exposed HTTP response headers, and WAFW00F identified the likely firewall technology.

Combining these tools provided a broader understanding of how reconnaissance can be performed using different information sources.

# CHAPTER 3: PM5 – NETWORK SCANNING USING ZENMAP

## 3.1 Introduction

Zenmap is the graphical interface for Nmap. It simplifies network scanning by providing predefined scanning profiles and graphical representations of discovered hosts.

The practical exercise focused on identifying the local network configuration and discovering active hosts.

## 3.2 Experimental Environment

The practical was performed using Kali Linux inside VirtualBox. The virtual machine used NAT Network mode.

| Parameter | Value |
|---|---|
| Interface | eth0 |
| IPv4 address | 10.0.0.2 |
| Subnet | 10.0.0.0/24 |
| Gateway | 10.0.0.1 |
| MAC address | 08:00:27:ab:5b:02 |

The information was collected using:
```bash
ip -br addr
ip route
ip link show eth0
```

## 3.3 Experiment 1: Zenmap Installation and Verification

Zenmap was already available in the Kali Linux environment.

**Command:**
```bash
zenmap --version
```

**Observed version:**
```text
zenmap 7.991
```

The executable was located at:
```text
/usr/bin/zenmap
```

## 3.4 Experiment 2: Single-Host Discovery

**Objective:** Verify host discovery against the local Kali virtual machine.

**Target:** 10.0.0.2  
**Profile:** Ping Scan

**Command:**
```bash
nmap -sn 10.0.0.2
```

**Observations:**

- Target host was reported as up.
- One IP address was scanned.
- One live host was discovered.
- Scan duration was approximately 0.50 seconds.

**Result:** Successful discovery of the local Kali virtual machine.

## 3.5 Experiment 3: Subnet-Wide Host Discovery

**Objective:** Perform host discovery across the configured virtual subnet.

**Target:** 10.0.0.0/24

**Command:**
```bash
nmap -sn 10.0.0.0/24
```

**Observations:**

| Parameter | Result |
|---|---|
| Subnet | 10.0.0.0/24 |
| Addresses scanned | 256 |
| Hosts reported up | 255 |
| Scan duration | 59.99 seconds |
| Scan type | Ping Scan |

The result was obtained from the Nmap completion summary.

**Important interpretation:** The unusually high number of hosts reported up requires caution. A virtual NAT Network may respond to discovery probes in ways that do not correspond to 255 independently operating computers. Therefore, the result is recorded as the scanner's reported count rather than a verified count of distinct physical or virtual machines.

## 3.6 Experiment 4: MAC Address Identification

The local Kali MAC address was identified using:
```bash
ip link show eth0
```

**Observed address:**
```text
08:00:27:ab:5b:02
```

Nmap also displayed the following MAC address for the gateway:
```text
52:54:00:12:35:00
```

The associated vendor identification was displayed as QEMU virtual NIC. These are separate observations and should not be interpreted as the same interface.

## 3.7 Experiment 5: Network Topology

Zenmap's Topology tab was used to visualize the discovered host. The initial single-host scan displayed the Kali virtual machine and its localhost reference. The subnet scan also populated the host list with numerous reported addresses.

The topology visualization was generated, but PDF export could not be completed successfully during the practical session. Available screenshots were retained as supporting evidence.

## 3.8 PM5 Summary

| Task | Outcome |
|---|---|
| Zenmap verification | Successful |
| Local IP identification | Successful |
| Subnet identification | Successful |
| Single-host discovery | Successful |
| Subnet-wide discovery | Executed |
| Host count | 255 reported up |
| MAC identification | Local MAC identified |
| Topology visualization | Generated |
| PDF export | Not completed |

## 3.9 Discussion

The experiment demonstrated the use of Zenmap and Nmap for identifying active hosts within a virtual network. The single-host scan provided a straightforward confirmation that the Kali virtual machine was reachable through the discovery process.

The subnet-wide scan produced a significantly larger number of responses than expected for a small virtual lab. This highlighted the importance of understanding network virtualization and validating automated scan results before drawing conclusions about the number of independent devices.

# CHAPTER 4: LIMITATIONS AND ETHICAL CONSIDERATIONS

The experiments were conducted for educational purposes.

The following limitations were observed:

1. The Zenmap topology PDF export could not be completed.
2. The subnet scan reported 255 hosts up, but the responses were not independently verified as separate devices.
3. MAC address information was not independently established for every reported host.
4. Some reconnaissance results represent tool-generated fingerprinting inferences rather than complete verification of underlying infrastructure.
5. No exploitation, credential attacks or unauthorized access attempts were conducted.

The exercises emphasized information gathering and network discovery rather than exploitation.

# CHAPTER 5: CONCLUSION

The Week 2 internship activities provided practical experience with fundamental cybersecurity reconnaissance and network discovery techniques.

Through PM1, six Kali Linux tools were used to examine domain registration information, web technologies, DNS records, HTTP headers and firewall characteristics.

Through PM5, the Kali Linux virtual machine's network configuration was examined, and Zenmap was used to perform both single-host and subnet-wide discovery.

The practical work also demonstrated the importance of interpreting automated security-tool outputs carefully, especially in virtualized network environments.

Overall, the exercises strengthened practical familiarity with reconnaissance utilities, DNS enumeration, HTTP inspection, firewall fingerprinting and network scanning.

# APPENDIX A: COMMAND REFERENCE

```bash
whois networkwalks.com
whatweb networkwalks.com
nslookup networkwalks.com
curl -I https://networkwalks.com
wafw00f networkwalks.com
dnsrecon -d networkwalks.com
zenmap --version
ip -br addr
ip route
ip link show eth0
nmap -sn 10.0.0.2
nmap -sn 10.0.0.0/24
```

# APPENDIX B: EVIDENCE CHECKLIST

**PM1**
- WHOIS output
- WhatWeb output
- Nslookup output
- cURL response headers
- WAFW00F output
- DNSRecon output

**PM5**
- Network interface configuration
- Routing information
- Zenmap installation verification
- Single-host Ping Scan
- Subnet-wide Ping Scan
- Host Details screenshot
- Network topology screenshot
- Topology PDF (not obtained)

**Final submission note:** The report records the experiments performed and their observed outcomes. Pending evidence and incomplete exports are explicitly identified rather than represented as completed work.
