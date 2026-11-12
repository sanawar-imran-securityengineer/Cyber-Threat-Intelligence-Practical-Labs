<p align="center">
  <img src="images/ai.png" alt="Cover" width="700">
</p>

# **Intelligence Reporting & Dissemination – KeepNote, WhoIs and IBM X-Force**

---

## **Table of Contents**

| **Section** |
| --- |
| [Overview](#overview) |
| [KeepNote Intelligence Notebook Setup](#keepnote-intelligence-notebook-setup) |
| [DNS Interrogation & WhoIs Lookup](#dns-interrogation--whois-lookup) |
| [IBM X-Force Exchange Threat Intelligence](#ibm-x-force-exchange-threat-intelligence) |
| [WannaCry Threat Intelligence Collection](#wannacry-threat-intelligence-collection) |
| [Cyber Threat Intelligence Report – WannaCry](#cyber-threat-intelligence-report--wannacry) |
| [Tools & Resources Summary](#tools--resources-summary) |
| [What I Learned](#what-i-learned) |
| [Conclusion](#conclusion) |

---

## **Overview**

This documentation covers **Intelligence Reporting and Dissemination** in **Cyber Threat Intelligence (CTI)**. It has three main activities: setting up a **KeepNote** notebook, **DNS interrogation** with a WhoIs lookup, and **malware threat analysis** with **IBM X-Force Exchange**.

| **Attribute** | **Details** |
| --- | --- |
| **Module** | Intelligence Reporting and Dissemination |
| **Target System** | www.certifiedhacker.com |
| **Network Range** | 172.17.217.1/24 |
| **Primary Tools** | KeepNote, IBM X-Force Exchange, WhoIs Lookup |
| **Threat Analyzed** | WannaCry Ransomware (MD5: 4c009243c755f658a3d4698cfa1272b8) |
| **TLP Classification** | TLP:AMBER |

---

## **KeepNote Intelligence Notebook Setup**

**KeepNote** is a free, open-source note-taking tool used by security professionals to organize findings. Here it was installed and structured to hold all **threat intelligence data**.

### **Step 1 – Installing KeepNote**

![Installing KeepNote](images/image1.png)

**Description:** The **KeepNote 0.7.8** setup wizard was started on the Windows machine. The welcome screen asks to close other applications, then **Next** moves the installation forward.

### **Step 2 – File Menu – New Notebook**

![File Menu – New Notebook](images/image2.png)

**Description:** In KeepNote the **File** menu was opened and **New Notebook…** was selected. This is the first **method** to create a fresh intelligence notebook.

### **Step 3 – Naming the Notebook**

![Naming the Notebook](images/image3.png)

**Description:** **Notebook1** was entered as the **notebook name** and the default save folder was kept. Clicking **New** finishes the creation.

### **Step 4 – Notebook Created**

![Notebook Created](images/image4.png)

**Description:** The workspace now shows **Notebook1** in the **left tree panel** next to the Trash folder. This confirms the notebook is ready to use.

### **Step 5 – Parent Folder Created**

![Parent Folder Created](images/image5.png)

**Description:** A parent folder named **Data Collection Through DNS Interrogation** was created. It appears in both the **tree panel** and the content area.

### **Step 6 – Parent and Child Folders**

![Parent and Child Folders](images/image6.png)

**Description:** A second folder, **Gathering IP and Domain Names**, was added. Both folders are visible in the tree and the content panel.

### **Step 7 – Folder Hierarchy**

![Folder Hierarchy](images/image7.png)

**Description:** The expanded tree shows the child folder **nested** under the parent folder. This **hierarchy** organizes all DNS intelligence data.

### **Step 8 – New Child Page Option**

![New Child Page Option](images/image8.png)

**Description:** A right-click on the **Gathering IP and Domain Names** folder opened the context menu. **New Child Page** (Shift+Ctrl+N) creates a page inside the selected folder.

### **Step 9 – whois lookup Page Created**

![whois lookup Page Created](images/image9.png)

**Description:** The child page **whois lookup** was created and now appears under the folder. It will store the **WhoIs results** for the target domain.

---

## **DNS Interrogation & WhoIs Lookup**

**DNS interrogation** is a passive **reconnaissance** technique that collects public information about a domain. A **WhoIs lookup** was performed on **certifiedhacker.com** and saved in KeepNote.

### **Step 10 – WhoIs Lookup Result**

![WhoIs Lookup Result](images/image10.png)

**Description:** A **WhoIs** website was used to search **certifiedhacker.com**. The result shows the **registration date, expiry date**, Bluehost **name servers** and the **client transfer prohibited** status.

### **Step 11 – WhoIs Data in KeepNote**

![WhoIs Data in KeepNote](images/image11.png)

**Description:** The WhoIs output was pasted into the **whois lookup** page. It holds **Domain Information, Registrar Information** and **Registrant Contact** details.

### **Step 12 – Export Notebook as HTML**

![Export Notebook as HTML](images/image12.png)

**Description:** From the **File** menu, **Export Notebook → HTML** was selected. This **method** turns the notebook into a web report that is easy to share.

### **Step 13 – Export Dialog**

![Export Dialog](images/image13.png)

**Description:** The **report name** and the **target save folder** were entered in the export dialog. Clicking **Export** generates the HTML report.

### **Step 14 – Exported Files**

![Exported Files](images/image14.png)

**Description:** The output folder contains **index.html, node.xml, notebook.nbk** and **tree.html** with page subfolders. These files make up the **portable report**.

### **Step 15 – HTML Report in Browser**

![HTML Report in Browser](images/image15.png)

**Description:** The **index.html** file was opened in a browser to verify the report. The left panel shows the **notebook tree** and the right panel shows the full **WhoIs data**.

### **Step 16 – Report, Client and Test Details**

![Report, Client and Test Details](images/image16.png)

**Description:** These tables show the **engagement metadata** of the CTI report, such as client organization and test dates. They summarize the **six-day assessment** timeline.

**WhoIs Intelligence Summary**

| **Field** | **Value** |
| --- | --- |
| **Domain** | certifiedhacker.com |
| **Registered On** | 2002-07-30 |
| **Expires On** | 2026-07-30 |
| **Updated On** | 2025-05-30 |
| **Status** | Client Transfer Prohibited |
| **Name Servers** | ns1.bluehost.com, ns2.bluehost.com |
| **Registrar** | Network Solutions, LLC |
| **IANA ID** | 2 |
| **Registrant Name** | PERFECT PRIVACY, LLC |

---

## **IBM X-Force Exchange Threat Intelligence**

**IBM X-Force Exchange** is a cloud **threat intelligence** sharing platform. This section covers **registration**, platform exploration and **malware analysis** of WannaCry.

### **Step 17 – Searching for X-Force Exchange**

![Searching for X-Force Exchange](images/image17.png)

**Description:** **exchange xforce ibm cloud** was searched in the browser. The top result is the **IBM X-Force Exchange** threat intelligence sharing platform.

### **Step 18 – IBM ID Registration Form**

![IBM ID Registration Form](images/image18.png)

**Description:** The **Create IBMid** form was filled with name, email, country and company details. The **Next** button moves to **email verification**.

### **Step 19 – Email Verification**

![Email Verification](images/image19.png)

**Description:** A **verification token** sent by email was entered in the token field. Clicking **Submit** completes the **IBM ID** account creation.

### **Step 20 – X-Force Main Dashboard**

![X-Force Main Dashboard](images/image20.png)

**Description:** After login the **dashboard** shows **Threat Analysis Reports** on the left and **OSINT Advisories** on the right. Recent entries include Hive0051 and QuirkyLoader.

### **Step 21 – Early Warning and Malicious Activity**

![Early Warning and Malicious Activity](images/image21.png)

**Description:** The **Early Warning Data** widget lists newly registered suspicious domains. The **Malicious Activity** counter showed **809 incidents** in the last hour, mostly **Spam**.

### **Step 22 – Malicious Activity World Map**

![Malicious Activity World Map](images/image22.png)

**Description:** The **world map** shows live threat distribution by country. **China** was the most active with **436 events** in the last hour, mainly **Spam**.

### **Step 23 – Map Snapshot – Central Asia**

![Map Snapshot – Central Asia](images/image23.png)

**Description:** A second snapshot of the map highlights **India** and **Kazakhstan** with **474 events**. It shows how **threat origins** change over time.

### **Step 24 – Public Collections Page**

![Public Collections Page](images/image24.png)

**Description:** The **Collections** page lists about **8,944 public collections** from the community. Entries such as **wikiworm.exe** and **MALWARE** show the variety of shared intelligence.

### **Step 25 – Phorpiex Botnet Collection**

![Phorpiex Botnet Collection](images/image25.png)

**Description:** The **Phorpiex Botnet Extortion Activity Monitoring** collection was opened. It has a **Summary**, **Background** on the **MaaS** model and **273 linked IP reports**.

### **Step 26 – Phorpiex IoC Reports**

![Phorpiex IoC Reports](images/image26.png)

**Description:** The IoC list shows **200 of 273 IP addresses** with **risk scores** from 5.7 to 10. Each entry has the **IP, analyst** and **date added**.

### **Step 27 – Malicious Activity Widget**

![Malicious Activity Widget](images/image27.png)

**Description:** This snapshot shows **397 events** in the last hour with **Spam** as the main category. **Scanning, Command and Control** and **Malware** events are also counted.

### **Step 28 – Recently Categorized Spam IPs**

![Recently Categorized Spam IPs](images/image28.png)

**Description:** The feed lists **recently categorized IP addresses** for Spam activity. The IPs come from **China, Kazakhstan, Pakistan** and other regions, which shows the **real-time** nature of the data.

### **Step 29 – IP Report for a Pakistani IP**

![IP Report for a Pakistani IP](images/image29.png)

**Description:** The **IP report** for 39.36.207.78 has a **risk score of 7.1**. It is categorized as **Spam, Dynamic IPs** and **Bots**, and the **WHOIS record** shows PTCL as the registrant.

### **Step 30 – Premium Reports – Threat Groups**

![Premium Reports – Threat Groups](images/image30.png)

**Description:** The **Premium Reports** page lists **Threat Group** profiles such as ITG25, TeamPCP and CyberAv3ngers. These reports give detailed **adversary profiling**.

### **Step 31 – Vulnerabilities Section**

![Vulnerabilities Section](images/image31.png)

**Description:** The **Vulnerabilities** section shows the latest global **CVEs**, including EZVIZ, HikCentral Pro and Pillow library issues. Each one is flagged with its **severity**.

### **Step 32 – CVE Vulnerability Report**

![CVE Vulnerability Report](images/image32.png)

**Description:** The report for **CVE-2026-32683** shows a **CVSS 3.1 score of 5.3** for EZVIZ products. The **attack vector** is Adjacent Network and the remedy is to **upgrade the app**.

### **Step 33 – Search Results for 'wiki'**

![Search Results for 'wiki'](images/image33.png)

**Description:** Searching **wiki** returned **584 results**. The left panel filters them by **observable type** such as Collection, Application and Vulnerability.

### **Step 34 – Scan File Option**

![Scan File Option](images/image34.png)

**Description:** The **Scan file** button on the search bar allows direct **malware file analysis**. The dashboard also shows the threat analysis and OSINT panels.

### **Step 35 – Selecting the Malware Sample**

![Selecting the Malware Sample](images/image35.png)

**Description:** The Windows **Open file** dialog was used to select the **WannaCry sample** for analysis. This **uploads** the file to the X-Force scan engine.

### **Step 36 – WannaCry Malware Report**

![WannaCry Malware Report](images/image36.png)

**Description:** The **malware report** for MD5 **4c009243c755f658a3d4698cfa1272b8** shows **High** risk. It is classified as **wannacry ransomware** for **Win32** with **92% coverage**.

### **Step 37 – WannaCry Hash Details**

![WannaCry Hash Details](images/image37.png)

**Description:** The side panel shows the core attributes: **MD5 hash, wannacry family, Ransomware type, 92% coverage** and **Win32 platform**. The sidebar links to Home, Activity, Collections and Groups.

### **Step 38 – Botnet Distribution Map**

![Botnet Distribution Map](images/image38.png)

**Description:** The **botnet map** for **qsnatch_a** shows **118 affected countries**. The **peak date** and an upward **trend arrow** point to a growing campaign.

### **Step 39 – Trending Botnets Panel**

![Trending Botnets Panel](images/image39.png)

**Description:** **qsnatch_a** is the top **High-risk** botnet with **371 impacted clients**. The panel also lists **Botnet C2 Servers** and linked collections.

### **Step 40 – IBM Security Intelligence Blog**

![IBM Security Intelligence Blog](images/image40.png)

**Description:** The **blog widget** on X-Force links to the **IBM Security Intelligence Blog**. The **Visit Security Intelligence Blog** button opens IBM's research articles.

### **Step 41 – Blog Security Section**

![Blog Security Section](images/image41.png)

**Description:** The blog's **Security** section shows featured articles such as **adversarial machine learning** and **security automation**. The **X-Force Threat Intelligence Index** is promoted in the sidebar.

### **Step 42 – IBM Security Products**

![IBM Security Products](images/image42.png)

**Description:** The **IBM security products** page includes **Guardium, watsonx.governance, Verify, HashiCorp** and **MaaS360**. These tools extend the **threat intelligence** workflow.

---

## **WannaCry Threat Intelligence Collection**

A private **WannaCry collection** was created on X-Force Exchange to store the gathered **IoCs** and findings. It documents the **threat type, protection steps** and **recommendations**.

### **Step 43 – Public Collections Overview**

![Public Collections Overview](images/image43.png)

**Description:** The **Public Collections** page shows about **8,948 entries** from many contributors. It is the starting point before creating a **private collection**.

### **Step 44 – My Collections – wanna cry**

![My Collections – wanna cry](images/image44.png)

**Description:** The **My Collections** tab shows the new **private** collection named **wanna cry**. The **+New Collection** card is also visible for more collections.

### **Step 45 – WannaCry Collection Details**

![WannaCry Collection Details](images/image45.png)

**Description:** The collection defines the **Threat Type** as ransomware targeting Windows. It lists the **MD5 hash**, **IoCs** like mssecsvc.exe, **protection** steps and **recommendations**.

### **Step 46 – Collection Details Panel**

![Collection Details Panel](images/image46.png)

**Description:** The right sidebar shows **Collection Details, Reports, Attachments, Linked Collections** and **Version History**. The **Sharing Options** button sets **TLP** and access.

### **Step 47 – Sharing Options**

![Sharing Options](images/image47.png)

**Description:** The dialog offers **Just me** (private) and **Share with others** modes. **TLP** is **NOT SPECIFIED** and public sharing is **Off** for **controlled dissemination**.

---

## **Cyber Threat Intelligence Report – WannaCry**

This formal **CTI report** summarizes the gathered intelligence: **executive summary, TLP classification, threat details, IoCs** and **recommended actions**.

**Executive Summary:** The assessment treated all infrastructure as **high-priority assets**. Findings show exposure to **private data disclosure** (IP addresses, domains, DNS details, source code) and **WannaCry ransomware**, plus risk of **social engineering** due to weak awareness training.

**Traffic Light Protocol Classification**

| **TLP Level** | **Count** | **Description** |
| --- | --- | --- |
| **HIGH (TLP:RED)** | 1 | Restricted to named recipients only – WannaCry ransomware IoCs |
| **MEDIUM (TLP:AMBER)** | 1 | Limited to the organization and trusted partners |
| **LOW (TLP:WHITE)** | 2 | Unrestricted public sharing – general awareness items |

**Threat Details**

| **Field** | **Details** |
| --- | --- |
| **Threat Code** | THR-001 |
| **TLP Rank** | TLP:AMBER |
| **Threat Name** | WannaCry |
| **Description** | Ransomware that encrypts files and spreads using SMB vulnerabilities |
| **Threat Capabilities** | File encryption, lateral movement, network propagation |
| **Threat Propagation** | Exploits SMBv1 vulnerability (MS17-010/EternalBlue) |
| **Target Victims** | Windows systems, enterprises, healthcare, government organizations |
| **Platform** | Win32 |
| **First Seen** | February 10, 2018 |
| **Last Seen** | May 9, 2026 |
| **Community Coverage** | 92% |

**Key Indicators of Compromise (IoCs)**

| **Threat Code** | **Threat Name** | **Indicator Type** | **Value** |
| --- | --- | --- | --- |
| THR-001 | WannaCry | MD5 Hash | 755f658a3d4698cfa1272b8 |
| THR-001 | WannaCry | File Name | mssecsvc.exe |
| THR-001 | WannaCry | File Extension | .WNCRY (encrypted files) |
| THR-001 | WannaCry | Network Activity | SMB traffic on TCP Port 445 |
| THR-001 | WannaCry | Ransom Note | @Please_Read_Me@.txt |
| THR-001 | WannaCry | Full Hash | 4c009243c755f658a3d4698cfa1272b8 |
| THR-001 | WannaCry | Kill Switch Domain | iuqerfsodp9ifjaposdfjhgosurijfaewrwergwea.com |

**Recommended Actions**

| **Priority** | **Action Item** | **Responsible Team** |
| --- | --- | --- |
| **Critical** | Apply MS17-010 Windows security patch on all unpatched systems immediately | IT / System Admins |
| **Critical** | Disable SMBv1 protocol across all Windows endpoints and servers | IT / Network Team |
| **High** | Deploy EDR monitoring rules to detect WannaCry behavioral indicators | SOC / Security Team |
| **High** | Implement offline backups and test restoration procedures | IT Operations |
| **High** | Distribute IoCs to SIEM, IDS/IPS, and endpoint detection platforms | SOC Team |
| **Medium** | Conduct phishing and social engineering awareness training for employees | HR / Security Awareness |
| **Medium** | Integrate IoCs into threat intelligence feeds for automated detection | Security Engineering |
| **Low** | Share threat intelligence report with SOC, IT, and management teams | CTI Analyst |

---

## **Tools & Resources Summary**

| **Tool / Resource** | **Purpose** | **URL / Location** |
| --- | --- | --- |
| **KeepNote 0.7.8** | Threat intelligence notebook and report organization | keepnote.org |
| **IBM X-Force Exchange** | IoC research, collections, malware analysis | exchange.xforce.ibmcloud.com |
| **WhoIs Lookup** | Domain registration intelligence gathering | whois.domaintools.com |
| **VirusTotal** | Malware hash verification and community analysis | virustotal.com |
| **Microsoft Defender TI** | Threat intelligence enrichment and correlation | Microsoft Security Portal |
| **SIEM / EDR Platforms** | Log correlation, endpoint behavioral monitoring | Organizational deployment |
| **IBM Security Blog** | Security research articles and threat advisories | securityintelligence.com |
| **IBM Guardium** | Data protection and vulnerability assessment | IBM Security Products portal |

---

## **What I Learned**

I learned how to install **KeepNote**, build a **folder structure** and **export** the notebook as an **HTML report**. I learned to run a **WhoIs lookup** for **DNS interrogation** and to explore **IBM X-Force Exchange**, including **collections, botnets, vulnerabilities** and **malware scanning**. I also learned to create a **private collection** and to use the **Traffic Light Protocol (TLP)** for responsible sharing.

## **Conclusion**

The full **intelligence reporting and dissemination** workflow was completed, from **notebook setup** and **domain intelligence** to **WannaCry analysis** and a final **CTI report**. The **WannaCry** threat (THR-001) was confirmed with its **MD5 hash**, **ransomware** classification and **92% community coverage**. The work shows the value of **structured documentation**, professional **threat intelligence platforms** and **TLP** for safe information sharing.
