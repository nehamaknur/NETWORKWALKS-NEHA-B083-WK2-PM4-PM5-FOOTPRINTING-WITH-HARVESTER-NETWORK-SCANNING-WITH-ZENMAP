# 🛡️ Penetration Testing Report: Footprinting & Network Scanning (theHarvester & Zenmap)

Building an authorized reconnaissance and mapping framework combining external OSINT collection via **theHarvester** and internal subnet discovery via **Zenmap**.

<p align="center">
  <img src="https://img.shields.io/badge/PROJECT-FOOTPRINTING_%26_SCANNING-blueviolet?style=for-the-badge">
  <img src="https://img.shields.io/badge/TARGETS-MICROSOFT.COM_%7C_10.138.53.0%2F24-orange?style=for-the-badge">
  <img src="https://img.shields.io/badge/OS-KALI_LINUX_%2F_WINDOWS-success?style=for-the-badge">
  <img src="https://img.shields.io/badge/TOOLKIT-THEHARVESTER_%2F_ZENMAP-informational?style=for-the-badge">
  <img src="https://img.shields.io/badge/SKILL-RECONNAISSANCE_%26_MAPPING-critical?style=for-the-badge">
  <img src="https://img.shields.io/badge/INTERNSHIP-NETWORKWALKS_B083-yellowgreen?style=for-the-badge">
  <img src="https://img.shields.io/badge/GITHUB-CORTEXNEHA-black?style=for-the-badge">
  <img src="https://img.shields.io/badge/AUTHOR-NEHA_MAKNUR-blue?style=for-the-badge">
</p>

---

| Field | Details |
| :--- | :--- |
| **Pentester Name** | Neha Maknur |
| **Batch** | B083 \| NetworkWalks Cybersecurity Internship |
| **Date** | 16 September 2026 |
| **Modules Completed** | W2-PM4: theHarvester-based Footprinting <br> W2-PM5: Network Scanning with Zenmap |
| **Client / Target** | 1. `networkwalks.com` (written permission secured) <br> 2. My own local VirtualBox host-only LAN |
| **Permission Secured** | ✅ Yes |
| **Phases Covered** | Phase 1: Footprinting & Reconnaissance with theHARVESTER <br> Phase 2: Network Scanning with Zenmap <br> Phase 3–5: In Progress |

---

## ⚠️ 1. Liability Disclaimer
I have performed these activities only on the systems & devices where I had secured written permission or the devices/systems that I own myself. All these materials are for education and research purpose only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries unauthorised access is a crime even when nothing is damaged.

---

## 📌 2. Introduction & Overview
This repository documents practical cybersecurity lab work completed as part of the Networkwalks internship program. The project covers two core phases:
1. **Footprinting & Reconnaissance with theHARVESTER**: Gathering public-facing intelligence, email addresses and subdomains on target domains using **theHarvester** on Kali Linux.
2. **Network Scanning with Zenmap**: Performing local subnet configuration checks via Windows `ipconfig`, live host enumeration, and topology mapping using **Zenmap**.

---

## 🛠️ 3. Tools & Technologies Used
| Tool / Technology | Purpose / Function |
| :--- | :--- |
| **Kali Linux** | Operating system environment utilized for running theHarvester command-line operations. |
| **Windows OS** | Local platform hosting Zenmap, command prompt (`cmd`), and local interface settings. |
| **theHarvester** | Open Source Intelligence (OSINT) reconnaissance tool used to gather emails, subdomains, and host data from public sources. |
| **Zenmap (Nmap GUI)** | Graphical user interface for Nmap used to execute ping sweeps, discover hosts, and map network topologies. |

---

## ⚙️ 4. Methodology & Execution

### Phase 1: Footprinting & Reconnaissance with theHARVESTER
* **Help & Usage Verification**: Inspected tool parameters and guidelines using command-line options (`theHarvester -h`) to understand syntax flags like domain selection (`-d`), result limits (`-l`), and data sources (`-b`).
* **Task 1 (Baidu Source Query)**: Executed targeted search against `microsoft.com` using the Baidu module with a result limit of 1000 and saving the text file as evidence using `cat task1.txt`:
  * **Execution Command**:
    ```bash
    theHarvester -d microsoft.com -l 1000 -b baidu
    ```
  * **Output Evidence**:
    ```bash
    cat task1.txt
    ```
  ![Task 1 Output Evidence](1-Screenshot-harvester-baidu-scan.png)
  
  * **Analysis & Objective**:
    * **What we are trying to prove**: Assesses how much organization-specific infrastructure is publicly discoverable via an eastern search engine module (`baidu`) without interacting directly with the target network.
    * **What is shown**: The output displays raw OSINT data harvested from Baidu, including discovered subdomains and associated IP addresses tied to `microsoft.com`.

* **Task 2 (Multi-Source Enumeration)**: Executed broader searches against `microsoft.com` using all available sources (`all`) with a result limit of 50 and saving the text file as evidence using `cat task2.txt`:
  * **Execution Command**:
    ```bash
    theHarvester -d microsoft.com -l 50 -b all
    ```
  * **Output Evidence**:
    ```bash
    cat task2.txt
    ```
  ![Task 2 Output Evidence](2-Screenshot-harvester-all-scan.png)
  
  * **Analysis & Objective**:
    * **What we are trying to prove**: Demonstrates the capabilities and limitations of automated multi-source enumeration (`all`), showing how the tool attempts to aggregate intelligence across a wide spectrum of public and proprietary OSINT feeds simultaneously.
    * **What is shown**: The output displays harvested asset data alongside explicit warning messages (`[-] API key missing`) for services such as **Bitbucket, Brave Search, Shodan, SecurityTrails, and others**. This proves that while public search modules execute successfully, restricted commercial or registration-bound modules are automatically bypassed due to unconfigured API credentials, limiting the scan strictly to free/unauthenticated data channels..

### Phase 2: Network Scanning with Zenmap

* Opened Windows Command Prompt and executed `ipconfig` to determine local interface configurations under the Wireless LAN adapter Wi-Fi (`IPv4 Address: 10.138.53.49`, `Subnet Mask: 255.255.255.0`, `Default Gateway: 10.138.53.36`).

![IP Configuration Output Evidence](3-Screenshot-ipconfig.png)

* Entered the local subnet range (`10.138.53.0/24`) into Zenmap, selected the **Ping scan** profile, and executed the underlying command:
  ```bash
  nmap -sn 10.138.53.0/24

 ![Ping Scan Output Evidence](4-Screenshot-Zenmap-pingscan.png)

   * **Zenmap Host Discovery Results**:
     * Executed the ping sweep command (`nmap -sn 10.138.53.0/24`) targeting the local subnet.
     * Successfully identified 2 active live hosts out of 256 scanned IP addresses (`10.138.53.36` and `10.138.53.49`) in 7.65 seconds.
     * Captured target MAC address details (`F2:4A:51:66:15:EA`) associated with the active gateway node.
  * **Network Topology Generation**:
    * Switched to the **Topology** tab in Zenmap to visually map discovered nodes relative to `localhost`.
    * Verified green node indicators confirming hosts with fewer than 3 open ports based on the active ping scan profile.
     
![Ping Scan Output Evidence](5-Screenshot-Zenmap-topology.png)

## 📋 Lab Assessment & Execution

Successfully completed and verified the Zenmap Network Scanning practice lab assessment, demonstrating practical proficiency in mapping network topologies and analyzing scan results.

![Practice Lab Score Assessment Result](6-Screenshot-Practice-lab-score.png)

## 🛡️ Consolidated Security Assessment & Risk Matrix

| # | Identified Vulnerability / Finding | Risk Rating | Remediation & Mitigation Strategy |
| :--- | :--- | :--- | :--- |
| **1** | External OSINT exposure of organizational metadata, emails, and surface footprints. | 🟠 Medium | Periodically audit and minimize the footprint of corporate identifiers and email addresses exposed on public search engines. |
| **2** | Enumeration of secondary web subdomains revealing additional surface endpoints. | 🟠 Medium | Maintain rigorous API configurations, secure backend intelligence endpoints, and restrict unnecessary public subdomains. |
| **3** | Unmonitored active hosts and open interfaces exposed during local subnet ping sweeps. | 🟠 Medium | Implement strict internal asset management inventories, firewall rules, and network access controls. |
| **4** | Operational syntax errors and incorrect network interface bindings during active phases. | 🟡 Low | Enforce strict syntax validation, double-check active `ipconfig` configurations, and maintain precise execution logs. |

## 🛠️ Challenges Encountered & Solutions

* **A. Network Interface Selection Discrepancy**
  * **Issue**: Initial attempts to define the Zenmap scan range mistakenly pulled parameters from an inactive virtual interface (`Ethernet adapter Ethernet` / `192.168.56.1`) instead of the live wireless connection.
  * **Resolution**: Re-ran the `ipconfig` utility to systematically trace the correct active medium (`Wireless LAN adapter Wi-Fi`), shifting the operational scope accurately to the `10.138.53.0/24` subnet.

* **B. Command-Line Precision & Syntax Errors**
  * **Issue**: During evidence logging, an attempt to inspect local text logs created via `cat` resulted in a syntax mistake (`tas1.txt` instead of `task1.txt`).
  * **Security Insight**: This minor typographical error immediately triggered file lookup exceptions, highlighting how absolute string precision and rigorous command habits dictate success in technical security operations.
  * 
## 🏁 Conclusion
This project successfully demonstrated the practical application of foundational reconnaissance and network discovery methodologies through structured security lab exercises. 

* **Footprinting & Reconnaissance**: Utilizing **theHarvester** on Kali Linux highlighted how OSINT techniques can effectively harvest target email addresses and map organizational attack surfaces from public-facing sources without interacting directly with target infrastructure.
* **Network Scanning**: Using **Zenmap** and Windows interface diagnostics (`ipconfig`) provided hands-on experience in identifying local subnets, executing ping sweeps, enumerating active live hosts, and mapping visual network topologies.
* **Operational Awareness**: Documenting challenges such as interface selection errors and command-line syntax precision reinforced the importance of meticulous execution and rigorous scope enforcement in professional security assessments.

Overall, the tasks completed under the Networkwalks Cybersecurity Internship successfully bridged theoretical concepts with practical defensive and offensive visibility principles.

## 🔗 Resources

- **Oracle VM VirtualBox 7.1.18** — ([Download Link](https://www.virtualbox.org/wiki/Downloads))
- **Kali Linux 2026.1** — ([Download Link](https://www.kali.org/get-kali/))
- **theHarvester** — Open-source intelligence (OSINT) and footprinting tool
- **Zenmap** —([Download Link](https://nmap.org/download.html))
- **7-Zip** — ([Download Link](https://www.7-zip.org/download.html))
- **GitHub** — ([GitHub Platform](https://github.com/))

---
# 👤 Author

**Neha Maknur**
B.Sc. Computer Science Graduate |
Aspiring Cyber Security Professional

LinkedIn: https://lnkd.in/p/dA5QnWVy

## 🗂️ Project Information

**Program Name:** Cybersecurity at Networkwalks | **Week:** 02 | **Project:** Penetration Testing Report: Footprinting & Network Scanning (theHarvester & Zenmap)| **Repository:** GitHub

