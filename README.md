# Azure-Sentinel-SIEM: Building a Honeypot with Azure Sentinel

Have you ever wondered how to gain hands-on experience with a robust SIEM like Azure Sentinel? I did too, and now I'm determined to make it happen by setting up my own Azure Sentinel homelab. This project involves creating a honeypot virtual machine that relays failed RDP attempts to Azure Sentinel, allowing us to explore this powerful tool firsthand while visualizing intrusion attempts on a world map!

### Steps to Set Up the Honeypot:

**Note: This Project Requires A Microsoft Azure Subscription!**

1. **Creating the Honeypot Virtual Machine:**

   - Create a new resource group (e.g., 'honeypot') and name your virtual machine (e.g., 'honeypot-vm').
   - Choose an appropriate region and select Windows 11 Pro as the OS.
   - Assign a strong password to the virtual machine, as it will be exposed to potential attacks.
   - Select an affordable VM size that supports at least 8GiB of RAM.
   - Customize networking settings:
     - Change `NIC network security group` from `basic` to `advanced`.
     - Configure an inbound rule to allow any incoming traffic with priority 100 for evaluation precedence.
     - Review and create the virtual machine.

   ![Create Honeypot VM](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/5cbff611-e487-4702-8596-0df13c723adb)

2. **Creating a Log Analytics Workspace:**

   - Create a Log Analytics Workspace in Azure to collect and analyze logs from our honeypot VM.
   - Configure data sources and ensure the workspace is connected to Azure Sentinel.
