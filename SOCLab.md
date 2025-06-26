# 🛡 homeSOClab  

**Home SOC Lab created using Azure's free subscription**

This project demonstrates how to deploy a functional cloud-based SOC using **Azure Sentinel**, **Log Analytics**, and a simulated **honeypot**.


![image](https://github.com/user-attachments/assets/ca7a885b-99a1-4c93-9267-7cd9631c029c)


---------------------------------------------------------------------

## ⚙ Environment Setup  
- **Platform:** Microsoft Azure (Free $200 budget)  
- **Resources Used:**
  - Windows 11 VM with open RDP (public IP) to attract attackers/bots  
  - Log Analytics Workspace  
  - Azure Sentinel  
  - Geo-IP CSV Watchlist  
  - Custom KQL queries and Workbooks

---------------------------------------------------------------------

##  Attack Simulation  
1. Deployed Windows VM with fully open NSG  
2. Waited for brute-force attacks from real-world sources to study how attackers behave 
3. Logs are collected via Log Analytics  
4. Azure Sentinel processed logs and generated alerts  
5. Geo-IP Watchlist mapped attacker IPs to locations on a world map

---------------------------------------------------------------------

##  Sample KQL Query
```kql
let GeoIPDB = _GetWatchlist("geoip");
SecurityEvent
| where EventID == 4625
| evaluate ipv4_lookup(GeoIPDB, IpAddress, network)
| summarize count() by IpAddress, cityname, countryname
```


## 🗺 Project Dashboard Visual Examples

![image](https://github.com/user-attachments/assets/f48b51a5-424f-4876-8f3f-5297d7aec183)
*Azure Sentinel map visualizing real outsider attack origins.*


## Learning Outcome

This project reinforced multiple practical skills and concepts relevant to real-world cybersecurity operations:

- Acquired hands-on experience configuring and monitoring a **cloud-based Security Operations Center (SOC)** using Azure Sentinel.
- Demonstrated how a publicly exposed virtual machine can serve as a **controlled honeypot** to collect telemetry on brute-force login attempts and malicious IP scanning activity, alongside attacker activity for training purposes.
- Leveraged **Log Analytics and KQL** to correlate failed authentication attempts with geolocation data from a custom **Geo-IP watchlist**, producing visual dashboards that aid threat attribution.
- Showcased the importance of **proactive threat hunting** by building and tuning queries that surface meaningful patterns from noisy log data.
- Reinforced the concept of **alert enrichment and context building**, critical for effective incident triage and response workflows.
- Gained insight into **cloud-native SIEM workflows**, including how Sentinel ingests data, triggers alerts, and supports automation through apps and playbooks.
  

------------------------------------------------------------------------


#  Azure Lab Infrastructure

![image](https://github.com/user-attachments/assets/4d2eb718-0185-4472-a221-0e26bb1a06a5)

The Windows 11 VM is hosted inside a typical Azure environment:

- **Azure Subscription** → Contains everything
- **Resource Group** → Organizes lab assets
- **Virtual Network (VNet)** → Connects resources privately
- **NSG (Network Security Group)** → Set with open rules for attacker visibility
- **Windows 11 VM** → Honeypot with public IP and RDP port exposed

🛑 *The NSG was intentionally misconfigured to allow inbound RDP (port 3389) from any source (0.0.0.0/0), simulating an exposed asset for attacker discovery.*


##  NSG Rule Configuration

![image](https://github.com/user-attachments/assets/c254e29a-eba6-4e31-9930-d81a01721f2f)


