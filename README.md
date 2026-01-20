# Azure-SOC-Honeypot-GeoIP-Abuse-Map
Azure-based SOC project focused on deploying a honeypot virtual machine exposed to the public internet, ingesting security telemetry into Microsoft Sentinel, and mapping observed abuse activity to global GeoIP data using a Sentinel Workbook.

## Objective

The objective of this project was to design and deploy a basic cloud SOC environment capable of detecting, ingesting, and visualising real-world abuse activity against a deliberately exposed virtual machine.

A vulnerable Azure VM was deployed within a controlled virtual network and left open to the public internet to attract reconnaissance and attack traffic. Security and system logs were collected into Azure Log Analytics and ingested into Microsoft Sentinel. Observed source IP addresses were enriched with GeoIP data and visualised using a Sentinel Workbook to demonstrate attacker distribution, attack volume, and geographic patterns.

This project was designed to simulate early-stage SOC monitoring tasks, reinforce SIEM fundamentals, and provide hands-on experience with cloud-based security telemetry, attack surface exposure, and security visibility.

### Skills Learned

- SIEM deployment, configuration, and log ingestion using Microsoft Sentinel
- Analysis of security and system event logs to identify malicious and anomalous activity
- Azure SOC architecture fundamentals (VNet, VM, Log Analytics Workspace, Sentinel)
- GeoIP enrichment and correlation of attacker source data
- Visualisation of security telemetry using Sentinel Workbooks
- Understanding common internet-facing attack patterns (scanning, brute force, probing)
- Strengthening defensive awareness around exposed services, firewalls, and access controls

### Tools Used

- Microsoft Azure (Subscription, Resource Groups, Virtual Network, Virtual Machine)
- Azure Log Analytics Workspace for centralized log ingestion
- Microsoft Sentinel (SIEM) for detection, querying, and visualisation
- KQL (Kusto Query Language) for log analysis and data extraction
- GeoIP enrichment using Sentinel native functions
- Sentinel Workbooks for interactive dashboards and abuse mapping

## Steps
&nbsp;
&nbsp;
<img width="1666" height="1113" alt="HONEYPOTATTACKMAPFINAL" src="https://github.com/user-attachments/assets/30e4612c-ab78-471a-af2c-93ba6a9c2db7" />
*Overview of project scope and network map.*

---


<img width="1019" height="1459" alt="scrnli_w27ti9I63lU57l" src="https://github.com/user-attachments/assets/c19095d7-1241-49dc-b9ff-b2f841035fae" />
*NSG being opened/disabled to allow all outside traffic - opening the honeypot.*

---


<img width="1939" height="1443" alt="scrnli_jR4ka5AfF22Wfo" src="https://github.com/user-attachments/assets/5c4abd88-259b-4152-9054-8e10b05f98c0" />
*Querying the forwarded logs from our VM, and searching for "4625 : Failed log on events - approximatly 13,000 events since opening up the VM to the net, highlighting the importance of proper defence and security controls.*

---


<img width="2490" height="1513" alt="scrnli_i8z63nYEn3LlvK" src="https://github.com/user-attachments/assets/d6bf7939-2fd3-4bbe-9298-11ee3a122b59" />
*Creating the GeoIP watchlist for data enrichment towards geomapping the abuse using a custom CSV of geo data.*

---


<img width="2478" height="1506" alt="scrnli_63RFCBnB13puCQ" src="https://github.com/user-attachments/assets/dfab4a96-6517-4966-ac45-7cd434e9cbe2" />
*Querying the newly enriched data using KQL - IpAddresses are now associated with a geographical location.*

---


<img width="2459" height="1495" alt="scrnli_jQXtCvzKd4bS9s" src="https://github.com/user-attachments/assets/f0d6cbd4-cd00-4712-b855-fb6589e985b3" />
*Isolating KQL searching to one IP result revealing 2,500 from this one IP - The volume, frequency, and uniformity of failed authentication attempts strongly indicate automated brute-force activity rather than manual interaction.*

---


<img width="2465" height="1526" alt="scrnli_0HpG23Msr8X27a" src="https://github.com/user-attachments/assets/4c926624-a239-4ab4-9725-a73ed3169210" />
*Creating the visual geomap of abuse IP locations, using JSON.*

---


<img width="2126" height="1512" alt="scrnli_UmMCO01oW1mJAb" src="https://github.com/user-attachments/assets/4c72da65-b7bb-4495-b63e-56a47d2e794c" />
*The workbook presented, showing a global network of various attacking locations.*

---


<img width="2434" height="1408" alt="AbuseEventID&#39;s" src="https://github.com/user-attachments/assets/fe7cf61c-1ace-4e6b-a779-c2a2f60d21ae" />
*KQL searching to investigate which EventID's were triggered on the system and forwarded to our workspace, this will aid showcasing actual attacker moves on the system, captured eventID's such as 4625 highly likely indicate brute force attemtps (due to the number of attempts), 4672 likely indicates elevated privlliages, 4798/99 indicate system reconnaissance, 5379/82 indicate credential access/manipulation, which all indicate intrusion behavior especially when grouped together - all triggered on the system within a 48hr period of being open to the public internet, automated attacks likely.*

---


<img width="2438" height="1436" alt="BruteForceCount" src="https://github.com/user-attachments/assets/7bf40c8e-875a-4862-9ec4-ba96ba8720a3" />
*Further KQL searching into brute force possibility confirms a match, with thousands of attempts originating from multiple different IP addresses.*

---
---

Stage 2 will involve; Creating Alerts & Automatically Generating Incidents (Analytics Rules)



