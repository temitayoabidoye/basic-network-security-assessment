Basic Network Security Assessment

Overview

This project documents a practical network security assessment performed in a controlled VirtualBox lab environment.

The assessment was conducted from the perspective of a Cybersecurity Analyst for a simulated small-office organization, SmallTech Solutions.

The objective was to identify exposed network services, review SSH security configuration, examine firewall settings, assess potential security risks, and provide recommendations for improving the security posture.

«Scope note: The practical assessment in this project was performed against a Kali Linux virtual machine in a controlled lab environment. It does not represent an assessment of a real production network or the entire simulated office environment.»

Objectives

- Identify the network configuration of the lab system.
- Discover open TCP and UDP services.
- Identify running services and versions.
- Review SSH security configuration.
- Examine inbound firewall configuration.
- Identify potential security weaknesses.
- Assess risk based on likelihood and impact.
- Provide practical security recommendations.

Methodology

The assessment followed these stages:

Discover → Identify → Analyze → Assess Risk → Recommend → Report

1. Network Discovery

The Kali Linux system was examined to identify its active network interface, IP address, and default gateway.

The primary interface identified during the assessment was:

- Interface: "eth0"
- IP address: "10.0.2.15/24"
- Default gateway: "10.0.2.2"

Connectivity to the gateway was verified successfully.

2. Port and Service Enumeration

Nmap was used to identify exposed TCP and UDP services.

The assessment included:

- Default TCP port scan
- Service and version detection
- Full TCP port scan
- Top 20 UDP ports

The scans identified:

- TCP 22 — SSH — Open
- The remaining TCP ports tested were closed.
- All of the top 20 UDP ports tested were closed.

Service detection identified:

- OpenSSH 9.3p2 Debian 1

The presence of a service version was treated as identification evidence and not automatically considered a vulnerability.

3. SSH Security Review

The SSH service was reviewed to determine how authentication and access were configured.

Key observations included:

- SSH service was active and running.
- SSH was listening on IPv4 and IPv6 wildcard addresses.
- Password authentication was enabled.
- Root password-based SSH login was restricted.
- Empty passwords were not permitted.
- "MaxAuthTries" was configured as 6.

The primary security concern identified was the continued availability of password-based SSH authentication.

4. Firewall Review

The host firewall configuration was examined using the available firewall tooling.

The inspected iptables INPUT chain showed:

- Default policy: "ACCEPT"
- No individual INPUT rules were listed.

This indicates that restrictive inbound rules were not observed in the inspected INPUT chain.

This finding does not by itself prove that the system is publicly exposed or that no other network-level security controls exist.

Key Findings

| Finding | Risk Level |
|---|---|
| SSH password authentication is enabled | Medium–High |
| No restrictive rules were observed in the inspected iptables INPUT chain | Medium |
| SSH listens on wildcard IPv4 and IPv6 interfaces | Medium |
| Root password-based SSH login is restricted | Positive control |
| Empty SSH passwords are disabled | Positive control |

Recommendations

1. Prefer SSH Key-Based Authentication

Configure and test secure SSH key-based authentication, then disable password authentication where appropriate.

This reduces exposure to password guessing and brute-force attacks.

2. Restrict SSH Access

Where practical, restrict SSH access to trusted hosts, networks, or administrative sources instead of allowing unrestricted inbound access.

3. Apply Restrictive Inbound Firewall Rules

Use a default-deny or otherwise restrictive inbound firewall policy and explicitly allow only required services.

4. Monitor SSH Authentication Activity

Review authentication logs and monitor for repeated failed login attempts or other suspicious SSH activity.

5. Review Exposed Services Regularly

Regularly scan systems for unnecessary open ports and services and disable services that are not required.

Tools Used

- Kali Linux
- Nmap
- OpenSSH
- ss
- iptables
- VirtualBox

Evidence

Technical evidence and assessment results are documented in the project report.

See:

"report/Project_2_Basic_Network_Security_Assessment_Report.pdf"

Skills Demonstrated

- Network reconnaissance
- Port scanning
- Service enumeration
- SSH security assessment
- Firewall configuration review
- Risk identification and assessment
- Security recommendations
- Technical security reporting
- Evidence-based analysis

Disclaimer

This assessment was performed in a controlled lab environment on an authorized virtual machine for educational and portfolio purposes. No unauthorized systems were targeted.
