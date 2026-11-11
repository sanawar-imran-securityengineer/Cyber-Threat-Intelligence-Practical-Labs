<div align="center">

# 🕵️ Cyber Threat Intelligence — Lab Reports 2.2 & 2.3

### Email Footprinting with EmailTrackerPro · DNS Interrogation with WHOIS & NSLookup

![Course](https://img.shields.io/badge/Course-Cyber%20Threat%20Intelligence-0b7285?style=for-the-badge)
![Topic](https://img.shields.io/badge/Topic-Footprinting%20%26%20Recon-364fc7?style=for-the-badge)
![Labs](https://img.shields.io/badge/Labs-2.2%20%2B%202.3-2b8a3e?style=for-the-badge)

</div>

---

## 📑 Table of Contents

1. [About the Author](#-about-the-author)
2. [Overview](#-overview)
3. [Objectives](#-objectives)
4. [Lab 2.2 — Email Footprinting](#-lab-22--data-collection-through-email-footprinting)
   - [Figures 2.2.1 – 2.2.11](#%EF%B8%8F-figure-221--edition-selection-after-installation)
   - [Findings — Lab 2.2](#-findings--lab-22)
   - [Conclusion — Lab 2.2](#-conclusion--lab-22)
5. [Lab 2.3 — DNS Interrogation](#-lab-23--data-collection-through-dns-interrogation)
   - [Figures 2.3.1 – 2.3.8](#%EF%B8%8F-figure-231--whois-domain-lookup-home-page)
   - [Findings — Lab 2.3](#-findings--lab-23)
   - [Conclusion — Lab 2.3](#-conclusion--lab-23)
6. [Overall Findings](#-overall-findings)
7. [Key Learnings](#-key-learnings)
8. [Tools Used](#-tools-used)
9. [Repository Structure](#-repository-structure)
10. [Disclaimer](#%EF%B8%8F-disclaimer)

---

## 👤 About the Author

| | |
|---|---|
| **Name** | Sanawar Imran |
| **Roll No.** | 243633 |
| **Program** | BS Cyber Security (Section A) — Air University, Islamabad |
| **Semester** | 4th |
| **Submitted to** | Naveed Naeem Abbass |
| **Currently** | Founder, Provilance Technologies · Penetration Tester Intern |
| **Career goal** | SOC Analyst / Detection Engineer (CTI specialization) |
| **Certifications** | ISC2 Candidate · Splunk Fundamentals 1 · EC-Council CTI · TryHackMe SOC Level 1 |

---

## 🧭 Overview

Footprinting is the first phase of any threat-intelligence or security assessment: collecting as much information as possible about a target **before** interacting with it directly. This repository documents two hands-on labs from the Cyber Threat Intelligence course that cover two common footprinting sources:

- **Lab 2.2 — Email footprinting:** a received email is traced back to its origin by analysing its raw headers with eMailTrackerPro.
- **Lab 2.3 — DNS interrogation:** WHOIS, NSLookup and passive DNS / threat-intel sources are used to collect registration, name-server and IP information about `www.certifiedhacker.com`.

Together, the two labs show how a few freely available tools can reveal the sender, route, ownership and infrastructure behind an email or a domain. Every step is backed by a screenshot with a short three-line description.

| Lab | Title | Tools |
|---|---|---|
| [Lab 2.2](#-lab-22--data-collection-through-email-footprinting) | Data collection through email footprinting | eMailTrackerPro, Gmail |
| [Lab 2.3](#-lab-23--data-collection-through-dns-interrogation) | Data collection through DNS interrogation | Whois, NSLookup, passive DNS / threat-intel sources |

---

## 🎯 Objectives

**Overall objective:** to practise passive and semi-passive reconnaissance techniques and learn how to turn raw data (email headers, WHOIS records, DNS answers) into usable threat intelligence.

**Lab 2.2 objectives**
- Retrieve the raw headers of a received email from Gmail ("Show original").
- Trace the email with eMailTrackerPro and follow the `Received:` chain hop by hop.
- Identify the sender IP, route, approximate location and signs of forgery.

**Lab 2.3 objectives**
- Collect registration data (registrar, dates, status, contacts) using WHOIS.
- Resolve the target's A record and name servers using NSLookup.
- Use passive DNS / threat-intel sources to see historical resolutions and the web-server banner.

---

## 📧 Lab 2.2 — Data Collection through Email Footprinting

| | |
|---|---|
| **Objective** | Trace a received email back to its origin by analysing its raw headers, and collect the sender IP, route and location. |
| **Tool** | eMailTrackerPro (Visualware) + Gmail "Show original" |
| **Figures** | 11 screenshots, each with a 3-line description |

#### 🖼️ Figure 2.2.1 — Edition selection after installation

<p align="center">
  <img src="images/screenshot1.png" width="800" alt="Edition selection after installation">
</p>

> **Description**<br>
> ① EmailTrackerPro shows the Edition Selection dialog the first time it is launched.<br>
> ② Standard traces emails and finds the sender's location; Advanced adds multi-trace, spam validation and misdirected-mail checks.<br>
> ③ The Advanced Edition (trial, day 3 of 15) is the edition used for this lab.

#### 🖼️ Figure 2.2.2 — Main window (My Inbox)

<p align="center">
  <img src="images/screenshot2.png" width="800" alt="Main window (My Inbox)">
</p>

> **Description**<br>
> ① The main window opens on the My Inbox tab, with a toolbar for Receive Mail, Whitelist, Blacklist, Filters, Search and Trace Email.<br>
> ② The message "No email accounts have been set up" appears because no mailbox is connected.<br>
> ③ This is fine, since the raw headers will be pasted into the tool manually.

#### 🖼️ Figure 2.2.3 — My Trace Reports tab

<p align="center">
  <img src="images/screenshot3.png" width="800" alt="My Trace Reports tab">
</p>

> **Description**<br>
> ① The My Trace Reports tab lists earlier traces and plots them on a world map.<br>
> ② The map is empty and the Trace Information panel is blank, because no email has been traced yet.<br>
> ③ Selecting a trace later will show its summary at the bottom of the window.

#### 🖼️ Figure 2.2.4 — Trace Headers dialog

<p align="center">
  <img src="images/screenshot4.png" width="800" alt="Trace Headers dialog">
</p>

> **Description**<br>
> ① Clicking Trace Headers opens the "eMailTrackerPro by Visualware" dialog.<br>
> ② The option "Trace an email I have received" is selected, as the goal is to locate the sender of a received email.<br>
> ③ The large box is where the copied raw email headers are pasted before pressing Trace.

#### 🖼️ Figure 2.2.5 — Selecting an email in Gmail

<p align="center">
  <img src="images/screenshot5.png" width="800" alt="Selecting an email in Gmail">
</p>

> **Description**<br>
> ① A suspicious promotional email titled "This Is Where the Money Is Flowing…" is found in the Gmail Spam folder.<br>
> ② Gmail flags it as similar to messages previously reported as spam; the sender name is "Dan Mirkin, CEO".<br>
> ③ The message menu is used to open the original message, which contains the full headers.

#### 🖼️ Figure 2.2.6 — Original message and raw headers

<p align="center">
  <img src="images/screenshot6.png" width="800" alt="Original message and raw headers">
</p>

> **Description**<br>
> ① Gmail's Original Message page lists the message ID, creation time, sender, recipient and subject.<br>
> ② Authentication checks are shown: SPF is PASS, DKIM is PASS and DMARC is PASS.<br>
> ③ The raw header text below (the Received: chain) is copied and pasted into eMailTrackerPro.

#### 🖼️ Figure 2.2.7 — Tracing started

<p align="center">
  <img src="images/screenshot7.png" width="800" alt="Tracing started">
</p>

> **Description**<br>
> ① After the headers are pasted, the trace begins and the status bar shows that the location is being looked up.<br>
> ② The world map and the Email Summary panel on the right start to fill with data.<br>
> ③ The tool walks through the Received: chain hop by hop to find the originating IP.

#### 🖼️ Figure 2.2.8 — Tracing complete — route and IP details

<p align="center">
  <img src="images/screenshot8.png" width="800" alt="Tracing complete — route and IP details">
</p>

> **Description**<br>
> ① The trace finishes and the route is drawn on the world map.<br>
> ② The IP Address Details panel shows IP, hostname, city, country, ISP and organisation for the traced address.<br>
> ③ The table at the bottom lists each hop, with its type (origin or private) and location.

#### 🖼️ Figure 2.2.9 — Hop table

<p align="center">
  <img src="images/screenshot9.png" width="800" alt="Hop table">
</p>

> **Description**<br>
> ① The hop table lists every hop in the email's path, numbered in order.<br>
> ② Hop 1 is a private address (192.168.40.2); the final hop is 149.72.173.41 on a udemy.com mail server host.<br>
> ③ The location column resolves the end hop to "America", matching the summary report.

#### 🖼️ Figure 2.2.10 — Email summary

<p align="center">
  <img src="images/screenshot10.png" width="520" alt="Email summary">
</p>

> **Description**<br>
> ① The summary shows From hello@alerts.udemy.com, To the author's mailbox, dated 16 Feb 2026, subject "You're in! Start your course today."<br>
> ② It reports location America, "Misdirected: Yes (possibly spam)" and a sender IP of 149.72.173.41.<br>
> ③ Header analysis notes an invalid timestamp, and a system scan shows no SMTP, HTTP, HTTPS or FTP server running.

#### 🖼️ Figure 2.2.11 — Identification report

<p align="center">
  <img src="images/screenshot11.png" width="640" alt="Identification report">
</p>

> **Description**<br>
> ① The final report says IP 149.72.173.41 was found, but little location detail was available, so the closest result is America.<br>
> ② It warns that an invalid timestamp suggests a forged header and that the sender address is easily faked, so it is not conclusive.<br>
> ③ A route map of North America shows the traced location; solid lines mark known hops and dotted lines mark guessed ones.

### 🔎 Findings — Lab 2.2

| Item | Result |
|---|---|
| Sender IP | `149.72.173.41` |
| Claimed sender | `hello@alerts.udemy.com` |
| Approximate location | America (closest location the tool could resolve) |
| Misdirected / possible spam | Yes |
| Header analysis | A timestamp claimed by a server on the route was not valid, so a header is suspicious |
| Open services | No SMTP, HTTP, HTTPS or FTP server running (ports closed) |
| Email authentication | SPF: PASS · DKIM: PASS · DMARC: PASS |
| First hop | Private address `192.168.40.2` |

> ⚠️ The sender address is easy to forge, so it should not be treated as conclusive on its own. Header analysis and the IP trace give stronger evidence.

### ✅ Conclusion — Lab 2.2
EmailTrackerPro is a good tool for email footprinting. It automates header analysis, shows the route on a map and saves a lot of time compared with reading headers by hand.

---

## 🌐 Lab 2.3 — Data Collection through DNS Interrogation

| | |
|---|---|
| **Objective** | Gather IP and domain information about `www.certifiedhacker.com` using WHOIS, NSLookup and public threat-intel sources. |
| **Tools** | Online Whois lookup, online NSLookup, passive DNS / threat-intel pages |
| **Figures** | 8 screenshots, each with a 3-line description |

#### 🖼️ Figure 2.3.1 — Whois domain lookup home page

<p align="center">
  <img src="images/screenshot12.png" width="800" alt="Whois domain lookup home page">
</p>

> **Description**<br>
> ① An online Whois service is opened to gather registration data for the target domain.<br>
> ② The search box accepts either a domain name or an IP address.<br>
> ③ This is the starting point for the domain and IP information gathering.

#### 🖼️ Figure 2.3.2 — Domain and registrar information

<p align="center">
  <img src="images/screenshot13.png" width="800" alt="Domain and registrar information">
</p>

> **Description**<br>
> ① The Whois record for certifiedhacker.com shows it was registered on 2002-07-30, expires 2026-07-30 and was last updated 2025-05-30.<br>
> ② The status is "client transfer prohibited" and the name servers are ns1.bluehost.com and ns2.bluehost.com.<br>
> ③ The registrar is Network Solutions, LLC (IANA ID 2), with an abuse e-mail and phone number listed.

#### 🖼️ Figure 2.3.3 — Registrant and technical contacts

<p align="center">
  <img src="images/screenshot14.png" width="800" alt="Registrant and technical contacts">
</p>

> **Description**<br>
> ① The registrant and technical contact sections of the same record are shown here.<br>
> ② Both are listed as Perfect Privacy, LLC in Jacksonville, FL, USA, a privacy-protection service.<br>
> ③ Personal details are masked, and the contact e-mail is a forwarding address at networksolutionsprivateregistration.com.

#### 🖼️ Figure 2.3.4 — NSLookup online tool

<p align="center">
  <img src="images/screenshot15.png" width="800" alt="NSLookup online tool">
</p>

> **Description**<br>
> ① An online NSLookup page is used to query the DNS records of the target.<br>
> ② The domain field is filled with www.certifiedhacker.com and the DNS server is set to localhost.<br>
> ③ The query type is set to A (IPv4 address) to get the IP the domain resolves to.

#### 🖼️ Figure 2.3.5 — NSLookup A-record query and answer

<p align="center">
  <img src="images/screenshot16.png" width="800" alt="NSLookup A-record query and answer">
</p>

> **Description**<br>
> ① The same query is shown with the form and the result together.<br>
> ② The non-authoritative answer shows www.certifiedhacker.com is an alias (canonical name) of certifiedhacker.com.<br>
> ③ The domain resolves to the IPv4 address 162.241.216.11.

#### 🖼️ Figure 2.3.6 — NSLookup name-server (NS) query

<p align="center">
  <img src="images/screenshot17.png" width="700" alt="NSLookup name-server (NS) query">
</p>

> **Description**<br>
> ① The query type is changed to find the authoritative name servers of the domain.<br>
> ② The answer lists ns1.bluehost.com and ns2.bluehost.com as the name servers of certifiedhacker.com.<br>
> ③ This matches the name servers already seen in the Whois record.

#### 🖼️ Figure 2.3.7 — Whois record and passive DNS resolutions

<p align="center">
  <img src="images/screenshot18.png" width="520" alt="Whois record and passive DNS resolutions">
</p>

> **Description**<br>
> ① A threat-intelligence style source shows a Whois record with the registrar, name server and the created, changed and expiry dates.<br>
> ② Below it, DNS Resolutions lists dated IP addresses (for example 45.56.120.93 in 2015 and 13.248.169.48 in 2025).<br>
> ③ Historical resolutions like these show how the infrastructure behind a domain has changed over time.

#### 🖼️ Figure 2.3.8 — Port 80 HTTP banner

<p align="center">
  <img src="images/screenshot19.png" width="640" alt="Port 80 HTTP banner">
</p>

> **Description**<br>
> ① The port 80 section displays the raw HTTP response returned by the web server.<br>
> ② It shows HTTP/1.1 200 OK, the server software (openresty), the date, content type and a Content-Length of 114.<br>
> ③ The short HTML body runs a script that redirects the browser to a /lander/ page; links to View on OTX and ThreatMiner are given.

### 🔎 Findings — Lab 2.3

| Field | Value |
|---|---|
| Domain | `certifiedhacker.com` |
| Registered / Expires / Updated | 2002-07-30 / 2026-07-30 / 2025-05-30 |
| Status | client transfer prohibited |
| Name servers | `ns1.bluehost.com`, `ns2.bluehost.com` |
| Registrar | Network Solutions, LLC (IANA ID 2) |
| Registrant / Tech contact | Perfect Privacy, LLC (privacy-protected) |
| A record | `162.241.216.11` (`www` is a CNAME of the root domain) |
| Historical resolutions | e.g. `45.56.120.93` (2015), `13.248.169.48` (2025) |
| Web server banner | `HTTP/1.1 200 OK`, openresty, redirects to a `/lander/` page |

### ✅ Conclusion — Lab 2.3
WHOIS, NSLookup and passive DNS sources together give a quick picture of a target's ownership, registrar, name servers and IP addresses. This is the foundation of the reconnaissance phase.

---

## 📊 Overall Findings

| # | Finding | Lab |
|---|---|---|
| 1 | The email's final traced hop was `149.72.173.41`, resolved only to "America" (country-level accuracy). | 2.2 |
| 2 | The email claimed to come from `hello@alerts.udemy.com`, yet the tool flagged it as misdirected / possible spam and reported an invalid timestamp. | 2.2 |
| 3 | SPF, DKIM and DMARC all passed, yet the message still landed in Spam, so passing authentication alone does not prove an email is trustworthy. | 2.2 |
| 4 | The first hop was a private address (`192.168.40.2`), which is internal and cannot be geolocated. | 2.2 |
| 5 | `certifiedhacker.com` was registered in 2002, is managed by Network Solutions and uses Bluehost name servers. | 2.3 |
| 6 | The registrant's identity is hidden behind a privacy service (Perfect Privacy, LLC). | 2.3 |
| 7 | `www` is a CNAME of the root domain, which resolves to `162.241.216.11`. | 2.3 |
| 8 | The name servers from NSLookup matched the WHOIS record, which confirms the data is consistent. | 2.3 |
| 9 | Passive DNS shows the domain pointed at different IPs over time (2015 vs 2025). | 2.3 |

---

## 🧠 Key Learnings

**Email footprinting**
- Email headers hold the real routing evidence. The `Received:` chain is read from the bottom (origin) to the top (destination).
- The `From:` field is trivial to spoof, so conclusions must come from the headers and the IP trace, not the display name or address.
- IP geolocation is approximate. A result like "America" shows the limits of the technique and why it needs corroboration.
- SPF, DKIM and DMARC "PASS" confirms the mail was authorised by the sending domain's infrastructure. It does not mean the content is safe or wanted.
- Private IPs in a header (such as `192.168.x.x`) are internal hops and cannot be traced.

**DNS interrogation**
- WHOIS reveals registrar, creation / expiry dates, status and name servers, which are useful for judging how old and how established a domain is.
- Privacy-protection services mask the registrant, so ownership often has to be inferred from other data.
- NSLookup record types matter: **A** gives the IPv4 address, **NS** gives the authoritative name servers, and a **CNAME** shows aliases.
- Cross-checking tools (WHOIS vs NSLookup) is a simple way to validate data.
- Passive DNS gives history that a live lookup cannot, which helps an analyst track infrastructure changes and pivot to related indicators.
- HTTP banners expose server software and behaviour (for example redirects), which helps profile a target.

**General**
- Footprinting can be done passively and legally with public sources, and it is the basis for later phases of an assessment.
- Good CTI work means collecting from several sources, validating them against each other and clearly stating what is not conclusive.
- Documenting each step with screenshots and short descriptions makes the work reproducible and reportable, a habit that is central to SOC and CTI roles.

---

## 🧰 Tools Used

- **eMailTrackerPro** (Visualware) — email header tracing
- **Gmail** — retrieving original message headers
- **Whois** lookup service — domain registration data
- **NSLookup** (online) — DNS record queries
- Public threat-intel / passive DNS sources — historical resolutions and banners

## 📁 Repository Structure

```
CTI-Lab-Reports/
├── README.md
└── images/
    ├── screenshot1.png … screenshot11.png    # Lab 2.2 (email footprinting)
    └── screenshot12.png … screenshot19.png   # Lab 2.3 (DNS interrogation)
```

## ⚖️ Disclaimer

These labs were completed for **educational purposes** as part of the Cyber Threat Intelligence course. Only intentionally public test targets (`certifiedhacker.com`) and the author's own mailbox were used. Do not run these techniques against systems you do not own or have permission to test.

---

<div align="center">

**Sanawar Imran** · BS Cyber Security · Air University · Roll No. 243633

</div>
