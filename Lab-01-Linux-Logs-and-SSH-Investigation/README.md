# 🛡️ Lab 01 - Linux Logs and SSH Investigation

![Status](https://img.shields.io/badge/Status-Completed-success)
![Platform](https://img.shields.io/badge/Platform-Ubuntu%2024.04-orange)
![Attacker](https://img.shields.io/badge/Attacker-Kali%20Linux-red)
![Difficulty](https://img.shields.io/badge/Difficulty-Beginner-blue)

---

# Executive Summary

This lab demonstrates the fundamentals of Linux log analysis and Secure Shell (SSH) investigation within a Security Operations Center (SOC) home lab environment.

A virtual network was created using Ubuntu 24.04 and Kali Linux. Ubuntu acted as the target machine while Kali Linux simulated an attacker system. The lab focused on configuring SSH, verifying network connectivity, exploring Linux log files, generating failed authentication attempts, and analyzing system logs using native Linux tools.

The objective was to understand how authentication events are recorded and how security analysts can investigate login attempts using Linux logs.

---

# Objectives

- Configure Ubuntu and Kali Linux virtual machines
- Verify network communication between systems
- Install and configure the OpenSSH server
- Explore Linux log files
- Simulate failed SSH login attempts
- Analyze authentication logs
- Understand Linux system logging
- Gain practical SOC investigation experience

---

# Lab Environment

| Component | Details |
|-----------|----------|
| Host OS | Windows |
| Virtualization | VMware Workstation |
| Target Machine | Ubuntu 24.04 |
| Attacker Machine | Kali Linux |
| Network Type | NAT |
| Target Service | OpenSSH |
| Log Sources | auth.log, journalctl, syslog |

---

# Tools Used

| Tool | Purpose |
|------|----------|
| Ubuntu 24.04 | Target system |
| Kali Linux | Attack machine |
| OpenSSH Server | Remote access |
| journalctl | System log analysis |
| auth.log | Authentication logs |
| htop | System monitoring |
| ip | Network configuration |
| ping | Connectivity testing |

---

# Network Topology

```
                VMware Workstation

        ┌───────────────────────────────┐
        │                               │
        │     NAT Network               │
        │                               │
        └───────────────────────────────┘
                 │
        ┌────────┴────────┐
        │                 │
        │                 │
 Ubuntu 24.04         Kali Linux
192.168.159.130     192.168.159.129

        Target          Attacker
```

---

# Lab Workflow

1. Configure Ubuntu VM
2. Configure Kali VM
3. Verify IP addresses
4. Test connectivity
5. Install OpenSSH
6. Enable SSH service
7. Simulate failed login attempts
8. Analyze Linux logs
9. Document findings

---

# Step 1 - Verify Ubuntu IP Address

Command

```bash
ip addr
```

Purpose

Displays all network interfaces and their assigned IP addresses.

Result

Ubuntu was assigned the IP address **192.168.159.130**.

![Ubuntu IP](images/01-ubuntu-ip.jpg)

---

# Step 2 - Verify Kali Linux IP Address

Command

```bash
ip addr
```

Purpose

Displays Kali Linux network configuration.

Result

Kali Linux was assigned the IP address **192.168.159.129**.

![Kali IP](images/02-kali-ip.jpg)
