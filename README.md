# SOC Detection & Threat Hunting Lab

> A hands-on blue-team home lab documenting how common attacks look **on the wire and in the logs** — detected and investigated with **Snort IDS, Wazuh, and Splunk**.

![Focus](https://img.shields.io/badge/Focus-Blue%20Team%20%2F%20SOC-1f6feb)
![SIEM](https://img.shields.io/badge/SIEM-Splunk%20%7C%20Wazuh-success)
![IDS](https://img.shields.io/badge/IDS-Snort%203-orange)
![Platform](https://img.shields.io/badge/Platform-Kali%20%7C%20Ubuntu%20%7C%20VirtualBox-lightgrey)
![Purpose](https://img.shields.io/badge/Purpose-Educational-informational)

---

## 👋 About this repository

This repo is my personal **cybersecurity lab portfolio**. For each exercise I set up a small virtual network, generated realistic malicious traffic in a **controlled, isolated environment**, and then focused on the part that matters most in a real SOC role: **detecting, logging, and investigating** that activity.

Every lab follows the same loop a security analyst works through every day:

**Attack simulated → Telemetry captured → Detected in SIEM/IDS → Analyzed → Mitigations recommended**

The goal isn't to show that an attack "works" — it's to show that I can **see it, explain it, and defend against it**.

> ⚠️ **Disclaimer:** All work was performed on my own isolated lab VMs (host-only networking). Nothing here targets real systems. This repository is for **education and professional portfolio purposes only**.

---

## 🧰 Skills demonstrated

| Area | What I did |
|---|---|
| **SIEM & Log Analysis** | Wrote Splunk SPL queries, built detection logic and alerts, correlated events across hosts |
| **Intrusion Detection** | Authored custom Snort 3 rules, ran the sensor, triaged alerts, forwarded to Wazuh |
| **Threat Detection Engineering** | Turned attacker behavior into detection rules and alert thresholds |
| **Network Security** | Analyzed Layer 2–7 attacks (ARP, DNS, ICMP, HTTP) and their indicators |
| **Web App Security** | Reproduced OWASP-style web vulns in DVWA and traced them in web server logs |
| **Incident Analysis** | Built attack timelines and mapped evidence to detection sources |
| **Tooling** | Kali Linux, VirtualBox, Splunk Enterprise, Wazuh, Snort, Apache |

---

## 📂 Labs in this repository

### 1. Snort IDS → Wazuh Alert Pipeline
Built a network IDS on Kali with **custom Snort 3 rules**, ran it in passive mode, generated ICMP and HTTP traffic from a second VM, and **forwarded the alerts into Wazuh** for centralized monitoring.

- Custom rule writing (`alert icmp` / `alert tcp`, SID management)
- Snort IDS mode, alert formats (fast / full / JSON)
- Log forwarding and centralized triage in the Wazuh dashboard
- Correlation rules firing (e.g. "multiple IDS events from same source IP")

📄 `snort_with_explanations.docx`

### 2. Web Application Attack Detection in Splunk
Reproduced a set of classic **web application vulnerabilities in DVWA** and, for each one, identified **what it looks like in the web server access logs indexed by Splunk**.

Covered: Stored XSS, Reflected XSS, DOM-based XSS, CSRF, Insecure File Upload, SQL Injection — each documented with its procedure, observations, and the **log signature** an analyst would hunt for.

📄 `attack&Cgt.docx`

### 3. Network Attack Lab + Splunk Detection & Response
A full attack-to-detection write-up covering four network attack classes in an isolated lab, each paired with **Splunk detection queries, alert rules, and mitigation strategies**:

- **ARP spoofing / MITM** — detection via duplicate MAC / ARP anomalies
- **DNS spoofing** — detecting rogue responses and redirects in logs
- **SSH brute force** — failed-auth correlation and threshold alerting
- **ICMP flood (DoS)** — traffic-spike detection and rate-limiting defenses

Includes an **attack timeline**, detection indicators per OSI layer, and a **defense/mitigation section** for each attack.

📄 `Splunk_practical.docx`

---

## 🗺️ Lab architecture

```
            Host-Only Network (isolated, 192.168.202.0/24)
   ┌───────────────────┐        ┌───────────────────┐
   │   Kali Linux       │        │   Ubuntu           │
   │   (sensor /        │◄──────►│   (target /        │
   │    traffic source) │        │    victim)         │
   └─────────┬──────────┘        └─────────┬──────────┘
             │  Snort alerts / host logs    │
             ▼                              ▼
        ┌──────────────────────────────────────┐
        │     SIEM layer: Splunk + Wazuh         │
        │  detection rules · alerts · dashboards │
        └──────────────────────────────────────┘
```

---

## 🧪 Detection engineering highlights

- **Custom IDS signatures** rather than default rulesets — shows I understand rule anatomy, not just tool operation.
- **SPL detection queries** that convert raw logs into actionable alerts (brute-force thresholds, DNS anomalies, traffic floods).
- **Cross-layer thinking** — the same incident is traced from packet capture → IDS alert → SIEM event → analyst conclusion.
- **Blue-team mindset** — every offensive step is documented alongside its detection source and a recommended mitigation.

---

## 📈 What I learned

- How attacker actions translate into concrete log artifacts, and how to write detections for them.
- The difference between **detecting** and **blocking**, and where IDS, SIEM, and host hardening each fit.
- How to build a repeatable attack → detect → defend workflow that mirrors real SOC operations.

---

## 📬 Contact

I'm actively looking for **SOC Analyst / Cybersecurity / Blue Team** opportunities.
Feel free to reach out or browse the detailed write-ups above.

*Built in a personal home lab for learning and demonstration purposes.*
