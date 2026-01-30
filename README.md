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
<img width="1666" height="1113" alt="HONEYPOTATTACKMAPFINAL" src="https://github.com/user-attachments/assets/ccc9916b-cb64-4d3a-8d4f-bbb955e4d3f2" />
Overview of project scope and network map.

---


<img width="1029" height="1526" alt="scrnli_M8dRKkiVPlw0Zs" src="https://github.com/user-attachments/assets/a6a2d3c6-039b-41e6-8d0f-96da8db6e90c" />
NSG being opened/disabled to allow all outside traffic - opening the honeypot.

---


<img width="1939" height="1443" alt="scrnli_jR4ka5AfF22Wfo" src="https://github.com/user-attachments/assets/183babfd-0138-47e4-a7a4-97136b2ea11c" />
After creating a Log analytics work space, Configure the “Windows Security Events via AMA” connector and then create the DCR within sentinel.
Screenshot: Querying the forwarded logs from our VM, and searching for "4625 : Failed log on events - approximatly 13,000 events since opening up the VM to the net, highlighting the importance of proper defence and security controls.

---


<img width="2490" height="1513" alt="scrnli_i8z63nYEn3LlvK" src="https://github.com/user-attachments/assets/664312bb-bdbb-4502-b7a5-2e242643eccf" />
Creating the GeoIP watchlist for data enrichment towards geomapping the abuse using a custom CSV of geo data.

---


<img width="2478" height="1506" alt="scrnli_63RFCBnB13puCQ" src="https://github.com/user-attachments/assets/7f51ba1e-01bd-44bd-99ac-c4dda9a79db5" />
Querying the newly enriched data using KQL - IpAddresses are now associated with a geographical location.

---


<img width="2459" height="1495" alt="scrnli_jQXtCvzKd4bS9s" src="https://github.com/user-attachments/assets/6b6ccd6f-84bd-4e7f-83ef-9e2327f5342c" />
Isolating KQL searching to one IP result revealing 2,500 from this one IP - The volume, frequency, and uniformity of failed authentication attempts strongly indicate automated brute-force activity rather than manual interaction.

---


<img width="2465" height="1526" alt="scrnli_0HpG23Msr8X27a" src="https://github.com/user-attachments/assets/32ee4a50-b10a-4c75-b067-e0cef45a0d0c" />
Creating the visual geomap of abuse IP locations, using JSON.

---


<img width="2126" height="1512" alt="scrnli_UmMCO01oW1mJAb" src="https://github.com/user-attachments/assets/a100301a-cd3d-42d9-8102-7f87d08a7bbd" />
The workbook presented, showing a global network of various attacking locations.

---


<img width="2434" height="1408" alt="AbuseEventID&#39;s" src="https://github.com/user-attachments/assets/bdcb11c6-e73f-4b9a-a5bd-3bcabb4d4518" />
KQL searching to investigate which EventID's were triggered on the system and forwarded to our workspace, this will aid showcasing actual attacker moves on the system, captured eventID's such as 4625 highly likely indicate brute force attemtps (due to the number of attempts), 4672 likely indicates elevated privlliages, 4798/99 indicate system reconnaissance, 5379/82 indicate credential access/manipulation, which all indicate intrusion behavior especially when grouped together - all triggered on the system within a 48hr period of being open to the public internet, automated attacks likely.

The combination of these event types within 48 hours of internet exposure is consistent with automated intrusion attempts, particularly if volumes are abnormally high and sources are external/suspicious. However, investigation should confirm the context, sources, and patterns before definitively classifying as malicious. For example eventID 4672 can be triggered by scheduled tasks.

---


<img width="2438" height="1436" alt="BruteForceCount" src="https://github.com/user-attachments/assets/ce7b7b15-b2cc-4bb1-8d2a-22b33485e39c" />
Further KQL searching into brute force possibility confirms a match, with thousands of attempts originating from multiple different IP addresses.

---
---

**Stage 2** will involve; Creating Alerts & Automatically Generating Incidents (Analytics Rules)

