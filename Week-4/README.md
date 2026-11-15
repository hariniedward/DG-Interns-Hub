<div align="center">

<img src="../assets/dg-interns-hub.png" alt="DG Interns Hub" width="130">

# Week 4: SIEM in Practice, Splunk, Wazuh and Log Ingestion

**DG Interns Hub | Cybersecurity Internship**

<img src="../assets/kali.png" alt="Kali Linux" width="46"> &nbsp;
<img src="../assets/ubuntu.png" alt="Ubuntu" width="46"> &nbsp;
<img src="../assets/virtualbox.png" alt="VirtualBox" width="46"> &nbsp;
<img src="../assets/tryhackme.png" alt="TryHackMe" width="46"> &nbsp;
<img src="../assets/github.png" alt="GitHub" width="46">

![Splunk](https://img.shields.io/badge/Splunk%20Enterprise-10.6.1.1-111111?style=for-the-badge)
![Wazuh](https://img.shields.io/badge/Wazuh%20manager-4.14.10-555555?style=for-the-badge)
![Snort](https://img.shields.io/badge/Snort-3.12.2.0-111111?style=for-the-badge)
![Nmap](https://img.shields.io/badge/Nmap-7.991-555555?style=for-the-badge)
![Hydra](https://img.shields.io/badge/Hydra-9.7-111111?style=for-the-badge)
![Sysmon](https://img.shields.io/badge/Sysmon-15.22-555555?style=for-the-badge)
![Kali](https://img.shields.io/badge/Kali-Linux-111111?style=for-the-badge&logo=kalilinux&logoColor=white)
![TryHackMe](https://img.shields.io/badge/TryHackMe-2%20rooms%20at%20100%25-555555?style=for-the-badge&logo=tryhackme&logoColor=white)

</div>

---

| | |
|---|---|
| **Intern** | Harini E |
| **Intern ID** | DG/15/OCT/CYBER/040 |
| **Position** | Cyber Security Intern |
| **Week** | 4 |
| **Prepared** | 15 November 2026 |
| **Lab** | VirtualBox: Windows 11, Kali Linux, Ubuntu 26.04 LTS |

## 1. Overview

In Week 4, I built a small SIEM lab around Splunk Enterprise, sent my Windows, Sysmon and Linux logs into it, attacked my own Ubuntu virtual machine from Kali, and wrote detections that turn that activity into searches, alerts and a dashboard. I completed the theory notes, two TryHackMe rooms, six hands-on tasks, two cheat sheets and two LinkedIn posts. Task 3 (the full Wazuh install) was not done, because the hardware note in the task sheet allows one SIEM to be built fully, and I built Splunk. All tests ran only on my own lab machines, and I used free tools only.

| Part | Result |
|---|---|
| Theory notes | 8 notes, one file for each question |
| TryHackMe rooms | 2 rooms, both at 100% |
| Task 1: Install Splunk | Completed, Splunk running with the `lab` index (2 GB maximum) |
| Task 2: Ingest logs | Completed, Security, Sysmon and auth.log events searchable in `index=lab` |
| Task 3: Wazuh | Not done (hardware note). A Wazuh manager on Kali was used only to test the custom rule in Task 5 |
| Task 4: Attack to alert | Completed, the Hydra brute force and the Nmap scan both found in Splunk |
| Task 5: Detections | Completed, 5 SPL searches, 2 scheduled alerts, a 4-panel dashboard and Wazuh rule 100010 tested |
| Task 6: Triage notes | Completed, 3 notes |
| Task 7: Cheat sheets | Completed, 17 SPL entries and 10 alert entries |
| LinkedIn posts | 2 posts |

## Contents

1. [Overview](#1-overview)
2. [Folder map](#2-folder-map)
3. [Lab environment](#3-lab-environment)
4. [Theory notes](#4-theory-notes)
5. [TryHackMe rooms](#5-tryhackme-rooms)
6. [Hands-on tasks](#6-hands-on-tasks)
7. [Problems and solutions](#7-problems-and-solutions)
8. [Safety and privacy](#8-safety-and-privacy)
9. [What I learned](#9-what-i-learned)
10. [LinkedIn posts](#linkedin-posts)

## 2. Folder map

```
Week 4/
├── README.md                        This file
├── Week4-Report-Harini.pdf          Weekly report
├── Week4-Presentation-Harini.pptx   Weekly presentation
├── Notes/                           8 theory notes
├── Writeups/                        2 TryHackMe writeups
├── Findings/                        Screenshots of Tasks 1 to 5, attack-to-alert evidence, task6-triage-notes.pdf
├── Detections/                      The 5 SPL searches and the custom Wazuh rule
└── Cheat Sheet/                     task7-cheat-sheets.pdf (SPL commands, SIEM alerts)
```

## 3. Lab environment

<img src="../assets/virtualbox.png" alt="VirtualBox" width="36"> The machines are connected by a Host-only network, `192.168.56.0/24`. My laptop has about 7 GB of memory and little free disk space, which is why I built only one SIEM fully.

| Machine | Role | Address |
|---|---|---|
| Windows 11 laptop | Host machine: Splunk Enterprise, Universal Forwarder and Sysmon | 192.168.56.1 |
| Kali Linux VM (kali-lab) | Attacker machine (Hydra and Nmap), and the Wazuh manager used to test my custom rule | 192.168.56.101 |
| Ubuntu 26.04 LTS VM (ubuntu-lab) | Target machine, with a Universal Forwarder for auth.log and the Snort alert file, and Snort from Week 3 | 192.168.56.102 |

**Tools (all free):** Splunk Enterprise 10.6.1.1 (free trial), Splunk Universal Forwarder, Splunk Add-on for Sysmon, Sysmon 15.22 with the SwiftOnSecurity configuration, Wazuh manager 4.14.10, Snort 3.12.2.0, Hydra 9.7, Nmap 7.991, VirtualBox and Google Drive for desktop.

**Ingestion flow:** log source (Windows Security, Sysmon, auth.log) → Splunk Universal Forwarder → indexer (Splunk Enterprise, port 9997, index `lab`) → search head (Splunk Web, `localhost:8000`).

## 4. Theory notes

The eight notes are in the [`Notes`](Notes) folder, one file for each question:

| No. | Topic |
|---|---|
| 1 | What a SIEM is, its components and data flow, and SIEM compared with log management, SOAR and EDR |
| 2 | Log ingestion methods, and the Splunk Universal Forwarder compared with the Wazuh agent |
| 3 | SPL basics: search, where, stats, table, eval, timechart and rex |
| 4 | Wazuh architecture, how decoders and rules work, and the rule levels 0 to 15 |
| 5 | True positive, false positive, true negative, false negative, alert fatigue and tuning |
| 6 | Detection logic for an SSH or Windows brute force, mapped to MITRE ATT&CK T1110 |
| 7 | Correlation rules, thresholds, baselines and allowlists |
| 8 | SOC tiers, the alert lifecycle and the five questions of a triage note |

## 5. TryHackMe rooms

<img src="../assets/tryhackme.png" alt="TryHackMe" width="36"> Both rooms are completed at 100%. Each room has its own writeup in the [`Writeups`](Writeups) folder, with the completion proof.

| No. | Room | Level | Time | Link |
|---|---|---|---|---|
| 01 | Introduction to SIEM | Easy | 120 min | https://tryhackme.com/room/introtosiem |
| 02 | Splunk: Exploring SPL | Medium | 60 min | https://tryhackme.com/room/splunkexploringspl |

My public profile: https://tryhackme.com/p/hariniedward

## 6. Hands-on tasks

### Task 1: Install Splunk

- I installed Splunk Enterprise on my Windows laptop, which the task sheet allows.
- I created an index named `lab` with a 2 GB maximum size, and confirmed it had 0 events before sending any data.

Evidence: [`Findings`](Findings)

### Task 2: Ingest logs into Splunk

- I turned on receiving port 9997, installed the Universal Forwarder on Windows for the Security and Sysmon logs, and installed the Splunk Add-on for Sysmon.
- A second forwarder on the Ubuntu VM sends `/var/log/auth.log`.
- A search on `index=lab` shows Windows Security (8,382 events), Sysmon (25,181 events) and auth.log (62 events).

Evidence: [`Findings`](Findings)

### Task 3: Wazuh

I did not do this task. The hardware note says that if the machine is limited, one SIEM can be built fully, so I built Splunk. I have no Wazuh dashboard, enrolled agent or file integrity monitoring screenshots, and I have not claimed any. The only Wazuh work this week is the custom rule in Task 5, tested with a Wazuh manager (4.14.10) installed on Kali.

### Task 4: Attack to alert

<img src="../assets/kali.png" alt="Kali" width="30"> <img src="../assets/ubuntu.png" alt="Ubuntu" width="30">

| Attack | Command | What Splunk showed |
|---|---|---|
| SSH brute force (T1110.001) | `hydra -l ubuntu -P wordlist.txt ssh://192.168.56.102` | 14 events in auth.log (13 failed passwords and 1 accepted password) from 192.168.56.101. The valid password is hidden. |
| SYN scan (T1046) | `nmap -sS 192.168.56.102` | Ports 22 and 80 open, 998 closed. My Snort rule 1000004 gave 980 alerts from 192.168.56.101, with 980 ports probed. |

A SYN scan never logs in, so auth.log has nothing about it. I sent Snort's alert file to Splunk with the Ubuntu forwarder (sourcetype `snort_alert`), and extracted the fields with `rex`.

Evidence: [`Findings`](Findings)

### Task 5: Detections

<img src="../assets/github.png" alt="GitHub" width="30">

| No. | SPL search | MITRE |
|---|---|---|
| 1 | Failed logons per user (EventCode 4625) | T1110 |
| 2 | PowerShell process creation (Sysmon EventCode 1) | T1059.001 |
| 3 | New user account creation (EventCode 4720) | T1136 |
| 4 | SSH failures per source IP | T1110 |
| 5 | Rare parent-child process pairs | Supports T1059 |

- **Scheduled alerts:** "Lab - Windows Failed Logons 4625 (T1110)" (3 or more failures in 15 minutes, severity Medium) and "Lab - SSH Failed Logins per Source IP (T1110)" (5 or more failures in 15 minutes, severity High). Both run every 15 minutes.
- **Dashboard:** Lab - SOC Detections Dashboard, with four panels on the last 24 hours.
- **Wazuh rule 100010:** in `/var/ossec/etc/rules/local_rules.xml` on Kali. It fires at level 10 when base rule 5760 fires 5 times from the same source in 300 seconds (T1110). In `wazuh-logtest`, the first four lines matched rule 5760 and the fifth matched rule 100010. I tested it with a hand-typed log line, not a live event from the Ubuntu VM.

Files: [`Detections`](Detections)

### Task 6: Triage notes

Three notes, each answering who, what, when, where and why, with a verdict and a next step. All three are true positives, because I caused each of them myself.

| Alert | Verdict |
|---|---|
| SSH brute force (Hydra) | True positive, 13 failed logins followed by 1 successful login |
| Nmap SYN scan (Snort rule 1000004) | True positive, real SYN scan traffic from a single source |
| Repeated failed Windows logons (4625) | True positive, but self-generated test activity rather than a real attack |

File: `task6-triage-notes.pdf` in [`Findings`](Findings)

### Task 7: Cheat sheets

| Cheat sheet | Content |
|---|---|
| SPL Command, Meaning, Example | 17 entries |
| SIEM Alert, Likely Cause, First Check | 10 entries |

File: `task7-cheat-sheets.pdf` in [`Cheat Sheet`](Cheat%20Sheet)

## 7. Problems and solutions

| Problem | Solution |
|---|---|
| Limited laptop memory and disk space | I built Splunk fully and did not do the Wazuh install (Task 3), as the hardware note allows |
| Sysmon events had no parsed fields | The add-on's source name did not match mine, so I copied its rule block into a local `props.conf` and restarted Splunk |
| The Nmap scan did not appear in auth.log | I used my Snort rule 1000004 from Week 3 and sent Snort's alert file to Splunk |
| Snort 3 did not write an alert file | The `-l` option alone does not make `alert_fast` write to a file, so I started Snort with `--lua 'alert_fast = { file = true }'` |
| The Wazuh manager would not start | Kali's disk was full from large files in `/var/ossec/tmp`. I deleted them and switched vulnerability detection off in `ossec.conf` |
| Rule 100010 did not fire in the first test | It waited on base rule 5716, but this Wazuh version matched my line as 5760. I changed the base rule, restarted the manager and tested again |
| The Host-only addresses were lost after each VM restart | I added them again by hand after every restart |
| Ubuntu-lab's disk was nearly full (about 92% used) | The install on Ubuntu-lab reported that storage was full, so I installed the Wazuh manager on Kali instead |

## 8. Safety and privacy

- All attacks and tests ran only on my own virtual machines and my own laptop.
- Personal details such as the Windows username, the computer name, MAC addresses and passwords are hidden in the screenshots.
- The valid password found by Hydra is hidden.

## 9. What I learned

- A SIEM is only as useful as the logs it receives. The brute force showed up easily because Linux logs every failed password, but the scan was invisible until I added Snort as a second log source.
- Small details decide whether a detection works. A source name that did not match, or a base rule number that was one off, was enough to stop a parser or a rule.
- Testing a detection against something real, by running Hydra and Nmap myself, proved that the searches and the rule behave the way I expected.
- Limits: I did not build the full Wazuh stack, rule 100010 was tested with a hand-typed line, and the Splunk trial licence warns that scheduled searches stop when the trial ends.

## LinkedIn posts

- Concept post: https://lnkd.in/p/ggvXav-i
- Weekly post: https://lnkd.in/p/g3NHM9mp

---

<div align="center">

*Prepared by Harini for the DG Interns Hub Cyber Security Internship, Week 4.*

</div>
