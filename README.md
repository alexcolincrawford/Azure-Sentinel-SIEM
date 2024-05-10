# Azure-Sentinel-SIEM: Building a Honeypot with Azure Sentinel

Have you ever wondered how to gain hands-on experience with a robust SIEM like Azure Sentinel? I did too, and now I'm determined to make it happen by setting up my own Azure Sentinel homelab. This project involves creating a honeypot virtual machine that relays failed RDP attempts to Azure Sentinel, allowing us to explore this powerful tool firsthand while visualizing intrusion attempts on a world map!

### Steps to Set Up the Honeypot:

**Note: This Project Requires A Microsoft Azure Subscription & A Valid API Key For ipgeolcation**

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

3. **Configuring The Microsoft Defender For Cloud:**
   - Ensure that in `Data Collection`, `All Events` is selected.
   ![image](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/6e94ea0f-3f8d-4e07-9962-3cc5226a70cf)

4. **Exposing Honeypot To Malicious Actors:**
   - Connect to the VM via the provided IP. (Found within the properties of the VM, under `networking`)
   - Once connected, navigate to the `Windows Defender Firewall`.
   - Select `Windows Defender Firewall Properties`
   - Set `Firewall State` to `OFF` for the _Domain, Private, Public_ profiles.
      - **!! NOTE: ENSURE THAT YOUR ARE EXPOSING YOUR VM, NOT YOUR HOST DEVICE !!**
     ![image](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/7c03bfd2-358a-44f8-b486-7fb35b6e5154)

5. **Generating Log File:**

   - Use a [PowerShell script](https://github.com/joshmadakor1/Sentinel-Lab/blob/main/Custom_Security_Log_Exporter.ps1) to generate custom security logs for Azure Sentinel.
   - This script targets security events with event ID `4625` (Logon Failure), retrieves geolocation data (latitude, longitude, country, etc.) using ipgeolocation.io API, and stores the fetched data in a log file.
   - Start the script.
   
6. **Creating A Custom Log For Log File:**
   - Navigate to `Tables` in the LAW.
   - Click `create` -> `New custom log (MMA-based)`.
   - Pass in a copy of the `failed_rdp.log`
   - Ensure the `record delimiter` is `New line`
   - Set the collection path to `C:\ProgramData\failed_rdp.log`
      - **Why?:** This is where the logs are stored on the honeypot VM.
   - Name & create it!

6b. **Viewing Custom Log:**
   - Navigate to `Logs` in the LAW.
   - Create a new query and search for the newly created log as shown below.

   ![image](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/ba5f2eb8-12ea-4616-b1e9-6595d4623c1e)


     
4. **Creating A Azure Sentinel Workspace & Workbook:**
   - Navigate to `Sentinel`, create a new workspace.
   - Select `Workbook` -> `Add Workbook`
   - Edit the worrkbook; remove all elements in the created workbook.
   - Select `Add` -> `Add Query`
      - We must create a query that contain extract the data out of RawData into seperate columns
      - [This query](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/blob/main/azure_query) can be used to that exact thing.
   - As shown below, we have now extracted each field from the RawData

     ![image](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/e7d9e5a2-8440-4f9d-bd43-cf127ba5399a)



