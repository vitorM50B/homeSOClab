# 🛡️ homeSOClab  

**Home SOC Lab created using Azure's free subscription**

This project is inspired demonstrates how to deploy a functional cloud-based SOC using **Azure Sentinel**, **Log Analytics**, and a simulated **honeypot**.

---------------------------------------------------------------------

## ⚙️ Environment Setup  
- **Platform:** Microsoft Azure (Free $200 budget)  
- **Resources Used:**
  - Windows 10 VM with open RDP (public IP) to attract attackers/bots  
  - Log Analytics Workspace  
  - Azure Sentinel  
  - Geo-IP CSV Watchlist  
  - Custom KQL queries and Workbooks

---------------------------------------------------------------------

## 🔍 Attack Simulation  
1. Deployed Windows VM with fully open NSG  
2. Waited for brute-force attacks from real-world sources to study how attackers behave 
3. Logs are collected via Log Analytics  
4. Azure Sentinel processed logs and generated alerts  
5. Geo-IP Watchlist mapped attacker IPs to locations on a world map

---------------------------------------------------------------------

## 📊 Sample KQL Query
```kql
let GeoIPDB = _GetWatchlist("geoip");
SecurityEvent
| where EventID == 4625
| evaluate ipv4_lookup(GeoIPDB, IpAddress, network)
| summarize count() by IpAddress, cityname, countryname
```


## 🗺️ Project Dashboard Visual Examples

![image](https://github.com/user-attachments/assets/f48b51a5-424f-4876-8f3f-5297d7aec183)
*Azure Sentinel map visualizing real outsider attack origins.*


## 🧠 Learning Outcome

This project reinforced multiple practical skills and concepts relevant to real-world cybersecurity operations:

- Acquired hands-on experience configuring and monitoring a **cloud-based Security Operations Center (SOC)** using Azure Sentinel.
- Demonstrated how a publicly exposed virtual machine can serve as a **controlled honeypot** to collect telemetry on brute-force login attempts and malicious IP scanning activity, alongside attacker activity for training purposes.
- Leveraged **Log Analytics and KQL** to correlate failed authentication attempts with geolocation data from a custom **Geo-IP watchlist**, producing visual dashboards that aid threat attribution.
- Showcased the importance of **proactive threat hunting** by building and tuning queries that surface meaningful patterns from noisy log data.
- Reinforced the concept of **alert enrichment and context building**, critical for effective incident triage and response workflows.
- Gained insight into **cloud-native SIEM workflows**, including how Sentinel ingests data, triggers alerts, and supports automation through apps and playbooks.
  

