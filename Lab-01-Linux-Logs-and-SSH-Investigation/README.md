# 🔐 Lab 01 - Linux Logs and SSH Investigation

## 📌 Overview

This project documents the first lab of my SOC Home Lab journey.

The goal of this lab was to build a small virtual environment using Ubuntu and Kali Linux, configure SSH, explore Linux system logs, and investigate authentication events generated through SSH login attempts.

This lab provides practical experience with Linux administration, networking, and basic security monitoring concepts that are commonly used by Security Operations Center (SOC) analysts.

---

# 🎯 Objectives

- Configure Ubuntu and Kali Linux virtual machines
- Verify network connectivity
- Install and configure OpenSSH Server
- Explore Linux log files
- Investigate authentication logs
- Generate SSH authentication events
- Analyze failed login attempts
- Learn basic Linux administration commands

---

# 🖥️ Lab Environment

| Component | Details |
|-----------|----------|
| Hypervisor | VMware Workstation |
| Attacker Machine | Kali Linux |
| Target Machine | Ubuntu 24.04 |
| Operating System | Linux |
| Protocol | SSH |
| Log Source | systemd Journal |
| Network | NAT |

---

# 🧰 Tools Used

- Ubuntu 24.04
- Kali Linux
- VMware Workstation
- OpenSSH Server
- journalctl
- systemctl
- ip
- ping
- htop

---

# 🌐 Network Configuration

## Ubuntu

IP Address

```
192.168.159.130
```

Screenshot

![](images/01-ubuntu-ip.jpg)

---

## Kali Linux

IP Address

```
192.168.159.129
```

Screenshot

![](images/02-kali-ip.jpg)

---

# 🔍 Step 1 — Verify Connectivity

From Ubuntu

```bash
ping 192.168.159.129
```

Result

Successful communication with Kali Linux.

Screenshot

![](images/03-ubuntu-ping-kali.jpg)

---

From Kali

```bash
ping 192.168.159.130
```

Result

Successful communication with Ubuntu.

Screenshot

![](images/04-kali-ping-ubuntu.jpg)

---

# 📂 Step 2 — Explore Linux Log Directory

Navigate to the log directory.

```bash
cd /var/log
```

List available logs.

```bash
ls -lh
```

Important log files discovered

- auth.log
- syslog
- journal
- boot.log
- dpkg.log
- kern.log

Screenshot

![](images/05-log-directory.jpg)

---

# 🔎 Step 3 — Authentication Logs

Attempted to view authentication logs.

Command

```bash
sudo tail -20 /var/log/auth.log
```

Observation

The system uses systemd journal logging instead of storing authentication events directly inside auth.log.

Screenshot

![](images/06-auth-log.jpg)

---

# 🔧 Step 4 — Install OpenSSH Server

Update repositories.

```bash
sudo apt update
```

Install OpenSSH.

```bash
sudo apt install openssh-server
```

Initially, an installation error occurred because the package name was entered incorrectly.

Correct package

```
openssh-server
```

Screenshot

![](images/07-ssh-install.jpg)

---

# 🚀 Step 5 — Start SSH Service

Start SSH.

```bash
sudo systemctl start ssh
```

Enable SSH.

```bash
sudo systemctl enable ssh
```

Verify status.

```bash
sudo systemctl status ssh
```

Result

SSH service successfully started.

Screenshot

![](images/08-ssh-running.jpg)

---

# 🔍 Step 6 — Verify SSH Service

Command

```bash
sudo systemctl status ssh
```

Output confirmed

- Service Active
- Running
- Listening on Port 22

Screenshot

![](images/09-ssh-status.jpg)

---

# 🔐 Step 7 — Generate SSH Authentication Events

Using Kali Linux, attempted SSH login into Ubuntu.

Example

```bash
ssh ananthan@192.168.159.130
```

Several incorrect passwords were intentionally entered to generate authentication logs.

Purpose

To simulate failed authentication events for SOC log analysis.

---

# 📖 Step 8 — Investigate SSH Logs

View SSH logs.

```bash
sudo journalctl | grep sshd
```

Observed Events

- SSH service started
- SSH listening on Port 22
- Authentication failure
- Failed password
- Connection closed
- PAM authentication messages

Screenshot

![](images/10-ssh-failed-login.jpg)

---

# 📚 Step 9 — Explore System Journal

Command

```bash
sudo journalctl
```

Purpose

View complete system logs managed by systemd.

Screenshot

![](images/11-journalctl-logs.jpg)

---

# 📊 Step 10 — Monitor System Resources

Command

```bash
htop
```

Purpose

Monitor

- CPU
- RAM
- Running Processes

Screenshot

![](images/12-htop-system-monitor.jpg)

---

# 📖 Key Linux Commands Learned

```bash
ip addr

ping

cd /var/log

ls -lh

sudo apt update

sudo apt install openssh-server

sudo systemctl start ssh

sudo systemctl enable ssh

sudo systemctl status ssh

sudo journalctl

sudo journalctl | grep sshd

htop
```

---

# 🛡️ Skills Demonstrated

- Linux Administration
- Networking Fundamentals
- SSH Configuration
- Linux Log Analysis
- Authentication Investigation
- System Monitoring
- Troubleshooting
- Security Operations Fundamentals

---

# 📚 Lessons Learned

During this lab I learned how to:

- Configure SSH services
- Understand Linux logging mechanisms
- Analyze authentication failures
- Investigate SSH login attempts
- Verify network connectivity
- Navigate Linux log directories
- Monitor Linux system resources
- Troubleshoot Linux service issues

---

# 📈 Future Improvements

- Configure Wazuh Agent
- Send logs to Wazuh Manager
- Create detection rules
- Perform brute-force simulations
- Integrate Sysmon for Linux
- Build a complete SOC monitoring environment

---

# 🏁 Conclusion

This lab provided hands-on experience with Linux administration, SSH configuration, authentication monitoring, and log analysis.

It forms the foundation of my SOC Home Lab and prepares the environment for future labs involving Wazuh SIEM, threat detection, log correlation, and incident investigation.

---

## 👨‍💻 Author

**Ananthan**

Cybersecurity Enthusiast

GitHub: https://github.com/ananthancyber

LinkedIn: https://linkedin.com/in/ananthan-d-ab295321b
