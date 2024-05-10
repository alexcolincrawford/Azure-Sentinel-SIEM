# Azure-Sentinel-SIEM: Building a Honeypot with Azure Sentinel

Have you ever wondered how to gain hands-on experience with a robust SIEM like Azure Sentinel? I did too, and now I'm determined to make it happen by setting up my own Azure Sentinel homelab. This project involves creating a honeypot virtual machine that relays failed RDP attempts to Azure Sentinel, allowing us to explore this powerful tool firsthand while visualizing intrusion attempts on a world map!

### Steps to Set Up the Honeypot:

**Note: This Project Requires A Microsoft Azure Subscription!**

1. **Creating the Honeypot Virtual Machine:**

   - Create a new resource group (e.g., 'honeypot') and name your virtual machine (e.g., 'honeypot-vm').
   - Choose an appropriate region and select Windows 11 Pro as the OS.
   - Assign a strong password to the virtual machine, as it will be exposed to potential attacks.
   - Select an affordable VM size that supports at least 8GiB of RAM.


   ![Create Honeypot VM](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/5cbff611-e487-4702-8596-0df13c723adb)

   - Customize networking settings:
     - Change `NIC network security group` from `basic` to `advanced`, as shown demonstrated below.
     ![image](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/c7dbd3ff-425f-4b02-8b09-75f76381bc4f)
     - Configure an inbound rule to allow any incoming traffic, by allowing all port ranges, with priority 100 for high priority.
     ![image](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/92eb28ec-63f4-4bdb-9629-cacc162aac3f)

     - Review and create the virtual machine.
     
   

2. **Creating a Log Analytics Workspace:**

   - Create a Log Analytics Workspace, name it apppropriately, and ensure it is within the same resource group as our VM.
   ![image](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/95f9a3c4-96d9-4bd9-b43c-20bacf9e199b)
