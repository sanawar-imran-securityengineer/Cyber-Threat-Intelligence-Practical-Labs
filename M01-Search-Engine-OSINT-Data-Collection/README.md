<div align="center">

<img src="images/ai.png" alt="Air University" width="700"/>

# 🕵️ Cyber Threat Intelligence: Lab Task Report

### Footholds • Files Containing Passwords • OSINT & Footprinting

![Course](https://img.shields.io/badge/Course-Cyber%20Threat%20Intelligence-blue?style=for-the-badge&logo=hackthebox&logoColor=white)
![Semester](https://img.shields.io/badge/Semester-4th-success?style=for-the-badge)
![Program](https://img.shields.io/badge/BS-Cyber%20Security-red?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-OSINT%20%26%20Recon-orange?style=for-the-badge)
![Tools](https://img.shields.io/badge/Tools-Nmap%20%7C%20Recon--ng%20%7C%20theHarvester-purple?style=for-the-badge)

</div>

---

## 📑 Table of Contents

- [1. 📌 Overview & Objectives](#1--overview--objectives)
- [2. 🎯 Task 1: Footholds (Google Hacking Database)](#2--task-1-footholds-google-hacking-database)
  - [2.1 Outdated Joomla 4.0.0 detected](#21-outdated-joomla-400-detected)
  - [2.2 CVE-2023-23752: Improper access control (Critical)](#22-cve-2023-23752-improper-access-control-critical)
  - [2.3 Credentials leaking through exposed files and indexes](#23-credentials-leaking-through-exposed-files-and-indexes)
  - [2.4 SQL injection risk in the export function](#24-sql-injection-risk-in-the-export-function)
- [3. 🔑 Task 2: Files Containing Passwords](#3--task-2-files-containing-passwords)
  - [3.1 Vulnerable files](#31-vulnerable-files)
  - [3.2 Files containing juicy information](#32-files-containing-juicy-information)
  - [3.3 Indexes of user files](#33-indexes-of-user-files)
- [4. 🛰️ Passive Intelligence Platforms](#4--passive-intelligence-platforms)
  - [4.1 ThreatCrowd](#41-threatcrowd)
  - [4.2 ZoomEye](#42-zoomeye)
  - [4.3 PublicWWW](#43-publicwww)
  - [4.4 DNSDumpster](#44-dnsdumpster)
- [5. 🍽️ Information Gathering on Zomato](#5--information-gathering-on-zomato)
  - [5.1 Dark-web searching](#51-dark-web-searching)
  - [5.2 Website footprinting](#52-website-footprinting)
  - [5.3 Passive subdomain enumeration](#53-passive-subdomain-enumeration)
  - [5.4 Google dorks](#54-google-dorks)
  - [5.5 Site map and free subdomain databases](#55-site-map-and-free-subdomain-databases)
  - [5.6 Active subdomain enumeration](#56-active-subdomain-enumeration)
  - [5.7 Directory and file discovery with ffuf](#57-directory-and-file-discovery-with-ffuf)
  - [5.8 DNS lookups, Amass and Shodan](#58-dns-lookups-amass-and-shodan)
  - [5.9 Nmap scanning](#59-nmap-scanning)
  - [5.10 Email footprinting with theHarvester](#510-email-footprinting-with-theharvester)
  - [5.11 Automated OSINT frameworks](#511-automated-osint-frameworks)
  - [5.12 Finding vulnerabilities with Nikto](#512-finding-vulnerabilities-with-nikto)
- [6. 📊 Summary of Findings](#6--summary-of-findings)
- [7. 🧰 Tools & Techniques Used](#7--tools--techniques-used)
- [8. 🛡️ Recommendations](#8--recommendations)
- [9. 🏁 Conclusion](#9--conclusion)
- [10. 📁 Repository Structure](#10--repository-structure)

---

## 1. 📌 Overview & Objectives

This report documents the hands-on **Cyber Threat Intelligence (CTI)** lab tasks completed for the 4th-semester CTI course. It covers two connected parts:

| Part | Focus |
|------|-------|
| **Task 1 / Task 2** | Finding *footholds* and *files containing passwords* with Google Hacking Database (GHDB) dorks, and enriching findings with passive-intel platforms |
| **Information Gathering** | Full OSINT / footprinting workflow against **zomato.com**: dark-web search, WHOIS and DNS, subdomain enumeration, Google dorks, port and service scanning, email harvesting, OSINT frameworks and vulnerability scanning |

**Learning goals**

- Understand how exposed files, indexes and misconfigurations become footholds
- Use search-engine dorks responsibly to discover sensitive exposure
- Perform passive and active reconnaissance and correlate results
- Document findings with evidence, in a repeatable way

## 2. 🎯 Task 1: Footholds (Google Hacking Database)

The **Footholds** category of the Google Hacking Database lists dorks that reveal pages and files which can give an attacker an initial way into a system.

<div align="center">

<img src="images/screenshot2.png" alt="screenshot2" width="80%"/><br/><br/>
<img src="images/screenshot3.png" alt="screenshot3" width="80%"/><br/><br/>
<sub><i>GHDB "Footholds" category and an exposed Joomla administrator directory index</i></sub>

</div>

### 2.1 Outdated Joomla 4.0.0 detected

The exposed manifest file of the `com_admin` component shows the site is running **Joomla 4.0.0**.

<div align="center">

<img src="images/screenshot4.png" alt="screenshot4" width="80%"/><br/><br/>
<sub><i>com_admin XML manifest exposing the exact Joomla version</i></sub>

</div>

> ⚠️ **This version is highly vulnerable.**
> `<creationDate>2006-04</creationDate>` is the project's *copyright* date, not the release date. **Joomla 4.0.0 was released on 17 August 2021**, so the site was installed around 2021–2022 and has not been updated since.

### 2.2 CVE-2023-23752: Improper access control (Critical)

| Field | Detail |
|-------|--------|
| **CVE ID** | CVE-2023-23752 |
| **Severity** | 🔴 Critical (CVSS 9.8) |
| **Affected versions** | Joomla! 4.0.0 – 4.2.7 |
| **Cause** | The REST API endpoint fails to properly validate permissions |
| **Impact** | Unauthenticated users can read sensitive configuration data such as database username, password and host |

Request pattern (from the analysis):

```http
GET /api/index.php/v1/config/application?public=true HTTP/1.1
Host: target.com
```

Adding `?public=true` bypasses the authorization check that normally restricts the endpoint to administrators, and the server returns a `200 OK` JSON body with configuration details.

<div align="center">

<img src="images/screenshot5.png" alt="screenshot5" width="60%"/><br/><br/>
<sub><i>CVE-2023-23752 vulnerability details and request analysis</i></sub>

</div>

### 2.3 Credentials leaking through exposed files and indexes

Dork results show how configuration files and open directory listings leak secrets.

| Evidence | What it shows |
|----------|---------------|
| Dork `"radius-server key" ext:cfg OR ext:log OR ext:txt` | Network device configs and logs exposing shared keys |
| Exposed `web.config` | Hard-coded impersonation username and password inside an IIS config |
| Exposed `config.inc.php` | Database host, name, username and password (highlighted) |
| `"index of" /wp-content/uploads/shell.php` | Open indexes where web-shell files are present |
| `/wp-content/plugins/dzs-videogallery/admin/` | Open plugin directory with an `upload` folder containing suspicious uploaded files |

<div align="center">

<img src="images/screenshot6.png" alt="screenshot6" width="80%"/><br/><br/>
<img src="images/screenshot7.png" alt="screenshot7" width="80%"/><br/><br/>
<img src="images/screenshot8.png" alt="screenshot8" width="80%"/><br/><br/>
<sub><i>Sensitive data exposed in search results, web.config and config.inc.php</i></sub>

</div>
<div align="center">

<img src="images/screenshot9.png" alt="screenshot9" width="80%"/><br/><br/>
<img src="images/screenshot10.png" alt="screenshot10" width="80%"/><br/><br/>
<img src="images/screenshot11.png" alt="screenshot11" width="80%"/><br/><br/>
<sub><i>Open directory listings: shell.php search and dzs-videogallery plugin folders</i></sub>

</div>

### 2.4 SQL injection risk in the export function

<div align="center">

<img src="images/screenshot12.png" alt="screenshot12" width="70%"/><br/><br/>
<sub><i>Plugin JavaScript where user-controlled slider data reaches a request</i></sub>

</div>

> The code uses `slidername` taken directly from HTML content, **without sanitization**, in a URL parameter that likely reaches a database query. This is a classic injection risk.

**Recommended fix:** validate and encode all input and use parameterized queries on the server side.

## 3. 🔑 Task 2: Files Containing Passwords

This task uses further GHDB categories to locate files that hold credentials or other sensitive information.

<div align="center">

<img src="images/screenshot13.png" alt="screenshot13" width="70%"/><br/><br/>
<sub><i>GHDB category: Files Containing Passwords</i></sub>

</div>

### 3.1 Vulnerable files

<div align="center">

<img src="images/screenshot14.png" alt="screenshot14" width="80%"/><br/><br/>
<img src="images/screenshot15.png" alt="screenshot15" width="80%"/><br/><br/>
<img src="images/screenshot16.png" alt="screenshot16" width="80%"/><br/><br/>
<img src="images/screenshot17.png" alt="screenshot17" width="80%"/><br/><br/>
<sub><i>GHDB category: Vulnerable Files, with dork searches and results</i></sub>

</div>

### 3.2 Files containing juicy information

<div align="center">

<img src="images/screenshot18.png" alt="screenshot18" width="80%"/><br/><br/>
<img src="images/screenshot19.png" alt="screenshot19" width="80%"/><br/><br/>
<img src="images/screenshot20.png" alt="screenshot20" width="80%"/><br/><br/>
<sub><i>GHDB category: Files Containing Juicy Info, with dork searches and results</i></sub>

</div>

### 3.3 Indexes of user files

Example dork: `intitle:"Index of" intext:"php" site:*.com.*`

<div align="center">

<img src="images/screenshot21.png" alt="screenshot21" width="80%"/><br/><br/>
<img src="images/screenshot22.png" alt="screenshot22" width="80%"/><br/><br/>
<img src="images/screenshot23.png" alt="screenshot23" width="80%"/><br/><br/>
<sub><i>Open directory indexes returned for PHP-related folders</i></sub>

</div>

## 4. 🛰️ Passive Intelligence Platforms

Public threat-intel and internet-scanning platforms enrich a target without touching it directly.

### 4.1 ThreatCrowd

Domain relationship graph, malicious-verdict votes and files that communicate with the domain.

<div align="center">

<img src="images/screenshot24.png" alt="screenshot24" width="80%"/><br/><br/>
<img src="images/screenshot25.png" alt="screenshot25" width="80%"/><br/><br/>
<img src="images/screenshot26.png" alt="screenshot26" width="80%"/><br/><br/>
<sub><i>ThreatCrowd domain analysis</i></sub>

</div>

### 4.2 ZoomEye

Search engine for internet-connected assets, services and banners.

<div align="center">

<img src="images/screenshot27.png" alt="screenshot27" width="80%"/><br/><br/>
<img src="images/screenshot28.png" alt="screenshot28" width="80%"/><br/><br/>
<img src="images/screenshot29.png" alt="screenshot29" width="80%"/><br/><br/>
<sub><i>ZoomEye search and results</i></sub>

</div>

### 4.3 PublicWWW

Source-code search engine used to find sites sharing specific code or signatures.

<div align="center">

<img src="images/screenshot30.png" alt="screenshot30" width="70%"/><br/><br/>
<sub><i>PublicWWW results</i></sub>

</div>

### 4.4 DNSDumpster

Maps hosting, networks, services and server banners for a domain.

<div align="center">

<img src="images/screenshot31.png" alt="screenshot31" width="80%"/><br/><br/>
<img src="images/screenshot32.png" alt="screenshot32" width="80%"/><br/><br/>
<img src="images/screenshot33.png" alt="screenshot33" width="80%"/><br/><br/>
<img src="images/screenshot34.png" alt="screenshot34" width="80%"/><br/><br/>
<sub><i>DNSDumpster results</i></sub>

</div>

## 5. 🍽️ Information Gathering on Zomato

Target for the OSINT exercise: **zomato.com**. The workflow below moves from the least intrusive techniques (dark-web and search-engine intelligence) to active scanning.

```text
Dark Web Search → WHOIS / DNS → Passive Subdomain Enum → Google Dorks
      → Site Map → Active Subdomain Enum → Port & Service Scan
      → Email Footprinting → OSINT Frameworks → Vulnerability Scan
```

### 5.1 Dark-web searching

After installing and connecting the **Tor Browser**, dark-web sources were searched for information about the target.

| Resource | Address |
|----------|---------|
| The Hidden Wiki: directory of `.onion` sites | `http://zqktlwi4fecvo6ri.onion/wiki/index.php/Main_Page` |
| Facebook's onion site: Facebook over Tor | `https://www.facebookcorewwwi.onion/` |

<div align="center">

<img src="images/screenshot35.png" alt="screenshot35" width="80%"/><br/><br/>
<img src="images/screenshot36.png" alt="screenshot36" width="80%"/><br/><br/>
<img src="images/screenshot37.png" alt="screenshot37" width="80%"/><br/><br/>
<img src="images/screenshot38.png" alt="screenshot38" width="80%"/><br/><br/>
<sub><i>Tor Browser, onion directory sites and the Facebook onion service</i></sub>

</div>

### 5.2 Website footprinting

**DNS record types reviewed**

| Record Type | Meaning |
|-------------|---------|
| **A** | IPv4 address |
| **AAAA** | IPv6 address |
| **MX** | Mail server |
| **NS** | Name servers |
| **TXT** | Extra info (SPF, verification) |
| **CNAME** | Aliases |

**WHOIS**: `whois zomato.com` returns the registrar (101domain GRS Limited), status flags and the AWS DNS name servers.

<div align="center">

<img src="images/screenshot39.png" alt="screenshot39" width="70%"/><br/><br/>
<sub><i>whois zomato.com</i></sub>

</div>

**DNS record collection**: `nslookup` and `dig` resolve the domain to several A records (18.138.28.22, 54.254.81.200, 13.228.182.224).

<div align="center">

<img src="images/screenshot40.png" alt="screenshot40" width="70%"/><br/><br/>
<img src="images/screenshot41.png" alt="screenshot41" width="70%"/><br/><br/>
<sub><i>`nslookup zomato.com` and `dig zomato.com`</i></sub>

</div>

### 5.3 Passive subdomain enumeration

Certificate-transparency logs (crt.sh) and other public sources reveal subdomains without sending traffic to the target.

<div align="center">

<img src="images/screenshot42.png" alt="screenshot42" width="80%"/><br/><br/>
<img src="images/screenshot43.png" alt="screenshot43" width="80%"/><br/><br/>
<img src="images/screenshot44.png" alt="screenshot44" width="80%"/><br/><br/>
<sub><i>crt.sh certificate-transparency search for zomato.com</i></sub>

</div>

### 5.4 Google dorks

Dorks used against the target:

```text
site:zomato.com filetype:pdf "menu"
site:zomato.com intitle:"index of"
site:zomato.com ext:js "api"
```

**Google results**

<div align="center">

<img src="images/screenshot45.png" alt="screenshot45" width="80%"/><br/><br/>
<img src="images/screenshot46.png" alt="screenshot46" width="80%"/><br/><br/>
<sub><i>filetype dork</i></sub>

</div>
<div align="center">

<img src="images/screenshot47.png" alt="screenshot47" width="80%"/><br/><br/>
<img src="images/screenshot48.png" alt="screenshot48" width="80%"/><br/><br/>
<img src="images/screenshot49.png" alt="screenshot49" width="80%"/><br/><br/>
<sub><i>intitle:"index of" dork</i></sub>

</div>

**Yahoo results** (a second engine for coverage)

<div align="center">

<img src="images/screenshot50.png" alt="screenshot50" width="70%"/><br/><br/>
<sub><i>Same dork on Yahoo</i></sub>

</div>

**`ext:js "api"`: JavaScript files that may reference API endpoints**

<div align="center">

<img src="images/screenshot51.png" alt="screenshot51" width="80%"/><br/><br/>
<sub><i>Google result</i></sub>

</div>
<div align="center">

<img src="images/screenshot52.png" alt="screenshot52" width="80%"/><br/><br/>
<sub><i>Yahoo result</i></sub>

</div>

### 5.5 Site map and free subdomain databases

**Site map of zomato.com**: each colour of the circle represents a domain or section; the rings show page paths from the root.

<div align="center">

<img src="images/screenshot53.png" alt="screenshot53" width="80%"/><br/><br/>
<img src="images/screenshot54.png" alt="screenshot54" width="80%"/><br/><br/>
<img src="images/screenshot55.png" alt="screenshot55" width="80%"/><br/><br/>
<img src="images/screenshot56.png" alt="screenshot56" width="80%"/><br/><br/>
<sub><i>Archive-based site map visualisations</i></sub>

</div>

**Free subdomain databases** (e.g. SecurityTrails DNS records)

<div align="center">

<img src="images/screenshot57.png" alt="screenshot57" width="80%"/><br/><br/>
<img src="images/screenshot58.png" alt="screenshot58" width="80%"/><br/><br/>
<img src="images/screenshot59.png" alt="screenshot59" width="80%"/><br/><br/>
<img src="images/screenshot60.png" alt="screenshot60" width="80%"/><br/><br/>
<img src="images/screenshot61.png" alt="screenshot61" width="80%"/><br/><br/>
<img src="images/screenshot62.png" alt="screenshot62" width="80%"/><br/><br/>
<sub><i>DNS records and subdomain lists from public databases</i></sub>

</div>

### 5.6 Active subdomain enumeration

Direct dictionary attack to discover subdomains.

**Sublist3r** (Python tool)

```bash
sudo apt update
sudo apt install sublist3r
sublist3r -d zomato.com
```

Sublist3r queried many search engines and services and found **52 unique subdomains**.

<div align="center">

<img src="images/screenshot63.png" alt="screenshot63" width="80%"/><br/><br/>
<img src="images/screenshot64.png" alt="screenshot64" width="80%"/><br/><br/>
<sub><i>Sublist3r basic enumeration</i></sub>

</div>

**Brute-force mode and port scanning of subdomains**

```bash
sublist3r -d zomato.com -p 80,443,8080,8443
```

<div align="center">

<img src="images/screenshot65.png" alt="screenshot65" width="80%"/><br/><br/>
<img src="images/screenshot66.png" alt="screenshot66" width="80%"/><br/><br/>
<sub><i>Sublist3r with port scan</i></sub>

</div>

**Real-time results**

<div align="center">

<img src="images/screenshot67.png" alt="screenshot67" width="80%"/><br/><br/>
<img src="images/screenshot68.png" alt="screenshot68" width="80%"/><br/><br/>
<sub><i>Live output while scanning</i></sub>

</div>

**Knockpy: Knock subdomain scanner**

<div align="center">

<img src="images/screenshot69.png" alt="screenshot69" width="60%"/><br/><br/>
<sub><i>Knockpy output</i></sub>

</div>

### 5.7 Directory and file discovery with ffuf

```bash
ffuf -w /usr/share/wordlists/dirb/common.txt -u https://zomato.com/FUZZ -v
```

<div align="center">

<img src="images/screenshot70.png" alt="screenshot70" width="80%"/><br/><br/>
<img src="images/screenshot71.png" alt="screenshot71" width="80%"/><br/><br/>
<sub><i>ffuf directory and file discovery, with status 301 redirects</i></sub>

</div>

### 5.8 DNS lookups, Amass and Shodan

**NS lookup and `dig zomato.com`**

<div align="center">

<img src="images/screenshot72.png" alt="screenshot72" width="80%"/><br/><br/>
<img src="images/screenshot73.png" alt="screenshot73" width="80%"/><br/><br/>
<img src="images/screenshot74.png" alt="screenshot74" width="80%"/><br/><br/>
<sub><i>Name-server and dig results</i></sub>

</div>

**Amass** (passive enumeration)

```bash
amass enum -passive -d zomato.com
```

<div align="center">

<img src="images/screenshot75.png" alt="screenshot75" width="80%"/><br/><br/>
<sub><i>Amass relationship graph: NS, MX, CNAME and netblocks</i></sub>

</div>

**Shodan** and **SSL certificate details**

<div align="center">

<img src="images/screenshot76.png" alt="screenshot76" width="80%"/><br/><br/>
<img src="images/screenshot77.png" alt="screenshot77" width="80%"/><br/><br/>
<sub><i>Shodan host view and SSL certificate details for AWS-hosted IPs</i></sub>

</div>

### 5.9 Nmap scanning

```bash
nmap -sV -sC zomato.com
nmap -p 80,443,22,21,8080 -sV zomato.com
```

| Port | State | Service |
|------|-------|---------|
| 21/tcp | filtered | ftp |
| 22/tcp | filtered | ssh |
| 80/tcp | open | http (AWS Elastic Load Balancing) |
| 443/tcp | open | ssl/http (AWS Elastic Load Balancing) |
| 8080/tcp | filtered | http-proxy |

The server header reveals **`awselb/2.0`**, so the site sits behind an AWS load balancer.

<div align="center">

<img src="images/screenshot78.png" alt="screenshot78" width="80%"/><br/><br/>
<img src="images/screenshot79.png" alt="screenshot79" width="80%"/><br/><br/>
<img src="images/screenshot80.png" alt="screenshot80" width="80%"/><br/><br/>
<sub><i>Nmap aggressive and service-detection scans</i></sub>

</div>
<div align="center">

<img src="images2/screenshot81.png" alt="screenshot81" width="80%"/><br/><br/>
<img src="images2/screenshot82.png" alt="screenshot82" width="80%"/><br/><br/>
<img src="images2/screenshot83.png" alt="screenshot83" width="80%"/><br/><br/>
<img src="images2/screenshot84.png" alt="screenshot84" width="80%"/><br/><br/>
<img src="images2/screenshot85.png" alt="screenshot85" width="80%"/><br/><br/>
<sub><i>Server header awselb/2.0 and further Nmap results</i></sub>

</div>

**DNS brute force with Nmap NSE**

```bash
nmap --script dns-brute zomato.com -oN zomato_subdomains.txt
```

<div align="center">

<img src="images2/screenshot86.png" alt="screenshot86" width="80%"/><br/><br/>
<img src="images2/screenshot87.png" alt="screenshot87" width="80%"/><br/><br/>
<sub><i>dns-brute discovering upload, mail, blog, www and mobile hosts</i></sub>

</div>

### 5.10 Email footprinting with theHarvester

Data collection through email footprinting.

```bash
theHarvester -d zomato.com -b all -f initial_harvest
```

<div align="center">

<img src="images2/screenshot88.png" alt="screenshot88" width="80%"/><br/><br/>
<img src="images2/screenshot89.png" alt="screenshot89" width="80%"/><br/><br/>
<img src="images2/screenshot90.png" alt="screenshot90" width="80%"/><br/><br/>
<img src="images2/screenshot91.png" alt="screenshot91" width="80%"/><br/><br/>
<img src="images2/screenshot92.png" alt="screenshot92" width="80%"/><br/><br/>
<img src="images2/screenshot93.png" alt="screenshot93" width="80%"/><br/><br/>
<img src="images2/screenshot94.png" alt="screenshot94" width="80%"/><br/><br/>
<sub><i>theHarvester collecting hosts, emails and IPs from multiple sources</i></sub>

</div>

### 5.11 Automated OSINT frameworks

**Recon-ng**

```bash
recon-ng
workspaces create zomato_recon
db insert domains    # domain: zomato.com
marketplace install all
```

<div align="center">

<img src="images2/screenshot95.png" alt="screenshot95" width="80%"/><br/><br/>
<img src="images2/screenshot96.png" alt="screenshot96" width="80%"/><br/><br/>
<img src="images2/screenshot97.png" alt="screenshot97" width="80%"/><br/><br/>
<img src="images2/screenshot98.png" alt="screenshot98" width="80%"/><br/><br/>
<img src="images2/screenshot99.png" alt="screenshot99" width="80%"/><br/><br/>
<sub><i>Recon-ng workspace, module installation and domains</i></sub>

</div>
<div align="center">

<img src="images2/screenshot100.png" alt="screenshot100" width="80%"/><br/><br/>
<img src="images2/screenshot101.png" alt="screenshot101" width="80%"/><br/><br/>
<img src="images2/screenshot102.png" alt="screenshot102" width="80%"/><br/><br/>
<img src="images2/screenshot103.png" alt="screenshot103" width="80%"/><br/><br/>
<sub><i>Recon-ng host results (community, zwstatic, mcp-server, zpay and more)</i></sub>

</div>

**SpiderFoot**: automated OSINT scan with correlations and data-type breakdown.

<div align="center">

<img src="images2/screenshot104.png" alt="screenshot104" width="80%"/><br/><br/>
<img src="images2/screenshot105.png" alt="screenshot105" width="80%"/><br/><br/>
<img src="images2/screenshot106.png" alt="screenshot106" width="80%"/><br/><br/>
<sub><i>SpiderFoot scan status, correlations and data types</i></sub>

</div>

### 5.12 Finding vulnerabilities with Nikto

```bash
nikto -h zomato.com
```

| Finding | Risk |
|---------|------|
| `X-Frame-Options` (anti-clickjacking) header **not present** | Site may be framed by other sites, enabling clickjacking |
| `X-Content-Type-Options` header **not set** | Browser may MIME-sniff content and render it unexpectedly |
| Server banner `awselb/2.0` | Technology disclosure |

<div align="center">

<img src="images2/screenshot107.png" alt="screenshot107" width="80%"/><br/><br/>
<img src="images2/screenshot108.png" alt="screenshot108" width="80%"/><br/><br/>
<sub><i>Nikto output: anti-clickjacking and X-Content-Type-Options findings</i></sub>

</div>

## 6. 📊 Summary of Findings

| # | Area | Key Result |
|---|------|------------|
| 1 | Joomla 4.0.0 | Outdated release (2021) vulnerable to **CVE-2023-23752** (CVSS 9.8) |
| 2 | Exposed files | Credentials and keys in `web.config`, `config.inc.php` and device configs |
| 3 | Open indexes | Directory listings exposing web-shell files and plugin folders |
| 4 | Code risk | Unsanitized `slidername` parameter, SQL injection risk |
| 5 | zomato.com DNS | A records resolve to AWS; AWS DNS name servers |
| 6 | Subdomains | **52** unique subdomains found with Sublist3r |
| 7 | Ports | 80 and 443 open; FTP, SSH and 8080 filtered |
| 8 | Headers | Missing `X-Frame-Options` and `X-Content-Type-Options` |

## 7. 🧰 Tools & Techniques Used

| Category | Tools |
|----------|-------|
| **Search-engine intel** | Google Hacking Database, Google dorks, Yahoo |
| **Threat-intel platforms** | ThreatCrowd, ZoomEye, PublicWWW, DNSDumpster, Shodan, SecurityTrails, crt.sh |
| **Dark web** | Tor Browser, Hidden Wiki, Facebook onion site |
| **DNS / WHOIS** | `whois`, `nslookup`, `dig` |
| **Subdomain enumeration** | Sublist3r, Knockpy, Amass, Nmap `dns-brute` |
| **Content discovery** | ffuf |
| **Scanning** | Nmap, Nikto |
| **OSINT frameworks** | theHarvester, Recon-ng, SpiderFoot |

## 8. 🛡️ Recommendations

1. Keep CMS platforms (Joomla, WordPress) and plugins **patched** to current versions
2. Disable **directory listing** and remove leftover files (shell, backup and config files) from web roots
3. Never store credentials in files reachable from the web; use environment variables or a secrets manager
4. Restrict sensitive API endpoints and enforce server-side authorization
5. Sanitize user input and use **parameterized queries**
6. Add security headers: `X-Frame-Options`, `X-Content-Type-Options`, CSP, HSTS
7. Hide server banners and version details
8. Monitor certificate-transparency logs and DNS for unexpected subdomains

## 9. 🏁 Conclusion

The lab shows how much can be learned about an organisation from public sources alone. Search-engine dorks, certificate logs, DNS data and OSINT frameworks quickly expose software versions, hosting details, subdomains and misconfigurations. A defender who runs the same reconnaissance on their own assets can find and fix these weaknesses before an attacker does.

> ⚠️ **Disclaimer:** This work was carried out for **educational purposes** as part of university coursework. Run scanning and enumeration techniques only against systems you own or have explicit written permission to test.

## 10. 📁 Repository Structure

```text
.
├── README.md
├── images/        # ai.png banner + screenshot2.png … screenshot80.png
└── images2/       # screenshot81.png … screenshot108.png
```

---

<div align="center">

### ⭐ Thanks for reading!

![Made by](https://img.shields.io/badge/Made%20by-Sanawar%20Imran-red?style=flat-square)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=flat-square)

</div>
