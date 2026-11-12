<p align="center">
  <img src="images/ai.png" alt="Banner" width="100%">
</p>

<div align="center">

# Cyber Threat Intelligence: Information Gathering Using Maltego

### OSINT Reconnaissance with Maltego Transforms

![Course](https://img.shields.io/badge/Course-Cyber%20Threat%20Intelligence-0b7285?style=for-the-badge)
![Tool](https://img.shields.io/badge/Tool-Maltego-364fc7?style=for-the-badge)
![Topic](https://img.shields.io/badge/Topic-OSINT-2b8a3e?style=for-the-badge)

</div>

---

## Table of Contents

1. [Overview](#overview)
2. [Objectives](#objectives)
3. [Setup and Login](#setup-and-login)
4. [Domain and DNS Reconnaissance](#domain-and-dns-reconnaissance)
5. [IP Address and Geolocation](#ip-address-and-geolocation)
6. [WHOIS Information](#whois-information)
7. [Person Information Gathering](#person-information-gathering)
8. [Findings](#findings)
9. [Conclusion](#conclusion)
10. [Key Learnings](#key-learnings)
11. [Tools Used](#tools-used)
12. [Repository Structure](#repository-structure)
13. [Disclaimer](#disclaimer)

---

## Overview

Open Source Intelligence (OSINT) is the collection of information from publicly available sources. Maltego is a graphical OSINT tool that turns a starting point, such as a domain name or a person, into a visual map of related data by running transforms against many public sources.

This repository documents a hands-on exercise from the Cyber Threat Intelligence course. It covers installing and logging in to Maltego, loading the data sources, and then running transforms to discover DNS records, mail servers, name servers, IP addresses, locations, WHOIS data and information about a person. Every step is backed by a screenshot with a short description.

---

## Objectives

- Launch Maltego, create an account and log in.
- Download the data sources and transform hubs needed for investigation.
- Add a domain entity to the canvas and run transforms against it.
- Discover DNS names, SOA, mail server (MX) and name server (NS) records.
- Resolve hostnames to IP addresses and find their geographic location.
- Collect WHOIS registration details for the domain.
- Gather public information about a person entity.

---

## Setup and Login

#### Figure 1: Launching Maltego

<p align="center">
  <img src="images/screenshot1.png" width="800" alt="Launching Maltego">
</p>

> **Description:** Maltego opens and shows its main splash screen. This confirms the tool is installed and ready to use.

#### Figure 2: Login screen

<p align="center">
  <img src="images/screenshot2.png" width="800" alt="Login screen">
</p>

> **Description:** The Maltego login screen is displayed. The user must sign in with registered credentials to access the platform.

#### Figure 3: Account registration

<p align="center">
  <img src="images/screenshot30.png" width="800" alt="Account registration">
</p>

> **Description:** A new Maltego account is created. The registration form is filled in to generate a new user ID.

#### Figure 4: Logging in to Maltego

<p align="center">
  <img src="images/screenshot40.png" width="800" alt="Logging in to Maltego">
</p>

> **Description:** The user logs in with the newly created credentials. Authentication succeeds and the Maltego workspace becomes available.

#### Figure 5: Maltego interface opened

<p align="center">
  <img src="images/screenshot5.png" width="800" alt="Maltego interface opened">
</p>

> **Description:** The main workspace is now fully open. It gives access to the entities, transforms and other tools available in the application.

#### Figure 6: Downloading data sources

<p align="center">
  <img src="images/screenshot6.png" width="800" alt="Downloading data sources">
</p>

> **Description:** The required data sources and transform hubs are being downloaded. This makes sure the needed plugins and intelligence feeds are available for analysis.

#### Figure 7: Fully loaded workspace

<p align="center">
  <img src="images/screenshot7.png" width="800" alt="Fully loaded workspace">
</p>

> **Description:** Maltego is completely loaded with all data sources integrated. The workspace is ready for information gathering.

---

## Domain and DNS Reconnaissance

#### Figure 8: Adding a domain name entity

<p align="center">
  <img src="images/screenshot8.png" width="800" alt="Adding a domain name entity">
</p>

> **Description:** A domain name entity is added to the canvas. This is the starting point of the reconnaissance and lets transforms run against the target domain.

#### Figure 9: Running transforms

<p align="center">
  <img src="images/screenshot9.png" width="800" alt="Running transforms">
</p>

> **Description:** Transforms are started on the domain entity. Maltego begins querying different sources for network and infrastructure information.

#### Figure 10: DNS transform started

<p align="center">
  <img src="images/screenshot10.png" width="800" alt="DNS transform started">
</p>

> **Description:** The DNS transform has started. Maltego is resolving the DNS records of the target domain to reveal its network infrastructure.

#### Figure 11: DNS name selection

<p align="center">
  <img src="images/screenshot11.png" width="800" alt="DNS name selection">
</p>

> **Description:** The DNS name results are shown and the relevant names are selected. These records give information about the subdomains and hostnames linked to the target.

#### Figure 12: DNS enumeration completed

<p align="center">
  <img src="images/screenshot12.png" width="800" alt="DNS enumeration completed">
</p>

> **Description:** The DNS enumeration is complete. All discovered DNS names are mapped on the canvas, giving a clear view of the domain's DNS structure.

#### Figure 13: Running the DNS Name SOA transform

<p align="center">
  <img src="images/screenshot13.png" width="800" alt="Running the DNS Name SOA transform">
</p>

> **Description:** The DNS Name SOA (Start of Authority) transform is executed. It retrieves authoritative DNS server information for the target domain.

#### Figure 14: DNS SOA transform completed

<p align="center">
  <img src="images/screenshot14.png" width="800" alt="DNS SOA transform completed">
</p>

> **Description:** The SOA transform finishes successfully. The results show the authoritative name server and administrative details of the domain.

#### Figure 15: Running the mail server transform

<p align="center">
  <img src="images/screenshot15.png" width="800" alt="Running the mail server transform">
</p>

> **Description:** The mail server (MX record) transform is run against the domain. Maltego queries the MX records to find the email servers configured for the target.

#### Figure 16: Mail server results

<p align="center">
  <img src="images/screenshot16.png" width="800" alt="Mail server results">
</p>

> **Description:** The mail server transform is complete. The results show the mail servers and related infrastructure used to handle email for the domain.

#### Figure 17: Identifying name server information

<p align="center">
  <img src="images/screenshot17.png" width="800" alt="Identifying name server information">
</p>

> **Description:** The name server (NS record) transform is run. It identifies the DNS name servers responsible for resolving the target domain.

#### Figure 18: Name server results

<p align="center">
  <img src="images/screenshot18.png" width="800" alt="Name server results">
</p>

> **Description:** The transform returns the name servers of the domain. These show which DNS providers manage the domain's DNS records.

---

## IP Address and Geolocation

#### Figure 19: Extracting IP address information

<p align="center">
  <img src="images/screenshot19.png" width="800" alt="Extracting IP address information">
</p>

> **Description:** IP address extraction is performed on the discovered entities. Maltego resolves the hostnames to their IP addresses for further geolocation and network analysis.

#### Figure 20: IP address details

<p align="center">
  <img src="images/screenshot20.png" width="800" alt="IP address details">
</p>

> **Description:** Detailed IP address information is retrieved. The results show the IP addresses mapped to the domain and its subdomains.

#### Figure 21: IP geolocation query

<p align="center">
  <img src="images/screenshot21.png" width="800" alt="IP geolocation query">
</p>

> **Description:** A geolocation transform is run on the identified IP address. Maltego queries location sources to find the physical location of the server.

#### Figure 22: IP location result

<p align="center">
  <img src="images/screenshot22.png" width="800" alt="IP location result">
</p>

> **Description:** The location of the IP address is identified. The result shows the country, region and city where the target server is hosted.

---

## WHOIS Information

#### Figure 23: WHOIS transform started

<p align="center">
  <img src="images/screenshot23.png" width="800" alt="WHOIS transform started">
</p>

> **Description:** The WHOIS transform is run to collect domain registration details. Maltego queries the WHOIS database for identity and registrar information linked to the domain.

#### Figure 24: WHOIS information retrieved

<p align="center">
  <img src="images/screenshot24.png" width="800" alt="WHOIS information retrieved">
</p>

> **Description:** The WHOIS data is retrieved. It includes registrant details, registration dates, registrar name and contact information for the target domain.

---

## Person Information Gathering

#### Figure 25: Gathering person information

<p align="center">
  <img src="images/screenshot25.png" width="800" alt="Gathering person information">
</p>

> **Description:** An investigation into a person entity is started. Maltego applies transforms to collect publicly available information about the individual.

#### Figure 26: Transform entities for a person

<p align="center">
  <img src="images/screenshot26.png" width="800" alt="Transform entities for a person">
</p>

> **Description:** Different transforms are applied to the person entity. They query social media, email and other OSINT sources to build a profile.

#### Figure 27: Person information gathered

<p align="center">
  <img src="images/screenshot27.png" width="800" alt="Person information gathered">
</p>

> **Description:** The person-based gathering is complete. The results map the individual's digital footprint, including associated emails, social accounts and other identifying information.

---

## Findings

| Area | Result |
|---|---|
| Starting entity | Domain name added to the Maltego canvas |
| DNS names | Subdomains and hostnames discovered and mapped on the canvas |
| SOA record | Authoritative name server and administrative details identified |
| Mail servers (MX) | Mail servers handling email for the domain identified |
| Name servers (NS) | DNS providers managing the domain's records identified |
| IP addresses | Hostnames resolved to their IP addresses |
| Geolocation | Country, region and city of the hosting server identified |
| WHOIS | Registrant details, dates, registrar and contact information retrieved |
| Person entity | Emails, social accounts and other identifiers mapped |

---

## Conclusion

Maltego makes OSINT investigations faster and easier to understand by running many lookups from one starting point and drawing the results as a graph. In this exercise it was used to map a domain's DNS, mail and name server infrastructure, find its IP addresses and location, collect WHOIS data and build a profile of a person, all from public sources.

---

## Key Learnings

- A single entity, such as a domain, can be expanded into a full map of related infrastructure by running transforms one after another.
- SOA, MX and NS records each reveal a different part of a domain: the authority, the mail servers and the DNS providers.
- Resolving hostnames to IP addresses allows further analysis such as geolocation, but the location shown is approximate.
- WHOIS data shows who registered a domain, when, and through which registrar.
- Person-based OSINT can reveal a wide digital footprint from public information alone.
- Results from transforms should be checked against other sources before they are treated as conclusive.
- Documenting each step with screenshots and short descriptions makes the work reproducible and reportable.

---

## Tools Used

- **Maltego**: OSINT and link analysis tool
- **Maltego Transform Hub**: data sources and transforms used for DNS, IP, location, WHOIS and person lookups

## Repository Structure

```
OSINT-Maltego/
├── README.md
└── images/
    ├── banner.png                              # Banner at the top of the README
    └── screenshot1.png … screenshot27.png      # Maltego steps
```

## Disclaimer

This exercise was completed for **educational purposes** as part of the Cyber Threat Intelligence course. Only information from public sources was used. Do not run these techniques against systems or people without permission to do so.
