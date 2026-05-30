# Azure Sentinel SIEM – RDP Honeypot & Live Attack Map

## Overview

This project involved deploying an intentionally exposed Windows 11 VM on Microsoft Azure to capture and analyse real-world RDP brute-force attempts. Failed login events (Event ID: #4625) were extracted via PowerShell, enriched with geolocation data, ingested into a Log Analytics Workspace, and visualised in real-time on a world map using Microsoft Sentinel.

The goal was to gain hands-on experience across the full detection pipeline — from log collection and data enrichment through to KQL querying and SIEM visualisation. _Refer to setup.md for the in-detail steps on configuration & setup_

---

## Results

Within **4–6 hours** of exposing the VM, the honeypot captured **8,669 failed RDP attempts** from across the globe:

| Source | IP | Attempts |
|---|---|---|
| India | 117.192.237.237 | 8,310 |
| Mexico | 187.134.7.165 | 342 |
| United Kingdom | 31.205.x.x | 10 |
| United Kingdom | 86.135.x.x | 4 |
| Panama | 194.165.16.76 | 2 |
| France | 46.105.132.55 | 1 |

The dominance of a single Indian IP — accounting for over 95% of all attempts — highlights how quickly automated scanning tools discover and hammer exposed RDP ports at scale.

![Live Attack Map](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/e8f9ea22-578f-427c-8edb-450fa6369188)

---

## Skills Demonstrated

- Microsoft Sentinel (SIEM) — workspace setup, workbook creation, map visualisation
- Azure Log Analytics Workspace — custom log ingestion (Microsoft Monitoring Agent based), KQL querying
- PowerShell — automated log generation targeting Event ID 4625
- Geolocation enrichment via ipgeolocation.io API
- Azure networking — NSG configuration, inbound rule management
- Honeypot deployment methodology

---

## How It Was Built

### 1. Honeypot VM Setup
Deployed a Windows 11 Pro VM in Azure within a dedicated resource group. The NIC network security group was set to Advanced, with a custom inbound rule permitting all traffic at priority 100 — intentionally maximising exposure to inbound scanning.

### 2. Log Analytics Workspace
Created a LAW in the same resource group as the VM. Microsoft Defender for Cloud was configured to collect All Events to ensure failed logon attempts were captured.

### 3. Firewall Disabled on VM
Connected to the VM via RDP and disabled Windows Defender Firewall across Domain, Private, and Public profiles — making the VM visible to external scanners.

### 4. PowerShell Log Generation
Deployed a PowerShell script targeting Event ID 4625 (Logon Failure). For each failed attempt, the script calls the ipgeolocation.io API to retrieve location data and appends enriched records to `C:\ProgramData\failed_rdp.log`.

### 5. Custom Log Ingestion
Configured a custom MMA-based log table in the LAW pointing to the log file path. This made the raw geolocation-enriched data queryable within Azure.

### 6. KQL Query & Data Extraction
Wrote a KQL query to parse the RawData field into structured columns (latitude, longitude, country, label, etc.), enabling map-based visualisation.
> Full query available [here](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/blob/main/azure_query)

### 7. Sentinel Workbook & Map
Created a Microsoft Sentinel workspace and workbook. Added a query-based tile, switched visualisation to Map, and configured metric labels — producing a live, auto-refreshing attack map.

---

## Key Takeaway

An exposed RDP port doesn't stay quiet for long. Over 8,300 attempts from a single IP within hours demonstrates the scale of automated credential-stuffing infrastructure operating continuously across the internet, reinforcing why network segmentation, strong authentication, and SIEM monitoring are non-negotiable in any production environment.

