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
2. Waited for brute-force attacks from real-world sources  
3. Logs collected via Log Analytics  
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
