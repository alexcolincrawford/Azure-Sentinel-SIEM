# Azure-Sentinel-SIEM: Building a Honeypot with Azure Sentinel

Have you ever wondered how to gain hands-on experience with a robust SIEM like Azure Sentinel? I did too, and now I'm determined to make it happen by setting up my own Azure Sentinel homelab. This project involves creating a honeypot virtual machine that relays failed RDP attempts to Azure Sentinel, allowing us to explore this powerful tool firsthand while visualizing intrusion attempts on a world map!

### Skills Gained
- Hands-on experience setting up and configuring Azure Sentinel SIEM.
- Understanding of honeypot deployment and log analysis techniques.
- Knowledge of Azure networking, security groups, and Log Analytics Workspace.
- Foundational Understanding of KQL.

### Tools Used

- Azure Sentinel SIEM
- Azure Virtual Machines
- Azure Log Analytics Workspace
- PowerShell scripting for log generation and automation

### Steps to Set Up the Honeypot:
**Note: This Project Requires A Microsoft Azure Subscription & A Valid API Key For ipgeolcation**

1. **Creating the Honeypot Virtual Machine:**
   - Create a new resource group (e.g., 'honeypot') and name your virtual machine (e.g., 'honeypot-vm').
   - Choose an appropriate region and select Windows 11 Pro as the OS.
   - Assign a strong password to the virtual machine, as it will be exposed to potential attacks.
   - Select an affordable VM size that supports at least 8GiB of RAM.
   ![Create Honeypot VM](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/5cbff611-e487-4702-8596-0df13c723adb)
   - Customize networking settings:
     - Change `NIC network security group` from `basic` to `advanced`.
     
     ![Advanced Networking](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/c7dbd3ff-425f-4b02-8b09-75f76381bc4f)
     - Configure an inbound rule to allow any incoming traffic, with priority 100 for high priority.
     ![Inbound Rule](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/92eb28ec-63f4-4bdb-9629-cacc162aac3f)
     - Review and create the virtual machine.
   

2. **Creating a Log Analytics Workspace:**

   - Create a Log Analytics Workspace, name it apppropriately, and ensure it is within the same resource group as our VM.
   ![LAW](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/95f9a3c4-96d9-4bd9-b43c-20bacf9e199b)

3. **Configuring The Microsoft Defender For Cloud:**
   - Ensure that in `Data Collection`, `All Events` is selected.
   ![All Events](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/6e94ea0f-3f8d-4e07-9962-3cc5226a70cf)

4. **Exposing Honeypot To Malicious Actors:**
   - Connect to the VM via the provided IP address (found within the VM properties under `networking`).
   - Once connected, navigate to the `Windows Defender Firewall`.
   - Select `Windows Defender Firewall Properties`
   - Set `Firewall State` to `OFF` for the _Domain, Private, Public_ profiles.
      - **!! NOTE: ENSURE THAT YOUR ARE EXPOSING YOUR VM, NOT YOUR HOST DEVICE !!**
     ![Firewall Rule](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/7c03bfd2-358a-44f8-b486-7fb35b6e5154)

5. **Generating Log File with PowerShell Script:**
   - Utilize a [PowerShell script](https://github.com/joshmadakor1/Sentinel-Lab/blob/main/Custom_Security_Log_Exporter.ps1) to generate custom security logs for Azure Sentinel.
   - The script targets security events with event ID `4625` (Logon Failure), retrieves geolocation data using ipgeolocation.io API, and stores the fetched data in a log file.
   - Execute the script.
   
6. **Creating a Custom Log for Log File:**
   - Navigate to `Tables` in the Log Analytics Workspace.
   - Click `create` -> `New custom log (MMA-based)`.
   - Set the collection path to `C:\ProgramData\failed_rdp.log`.
   - Name and create the custom log.

7. **Viewing Custom Log:**
   - Navigate to `Logs` in the LAW.
   - Create a new query and search for the newly created log as shown below.

   ![Custom Log](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/ba5f2eb8-12ea-4616-b1e9-6595d4623c1e)


     
8. **Creating A Azure Sentinel Workspace & Workbook:**
   - Navigate to `Sentinel`, create a new workspace.
   - Select `Workbook` -> `Add Workbook`
   - Edit the worrkbook; remove all elements in the created workbook.
   - Select `Add` -> `Add Query`
      - We must create a query that contain extract the data out of RawData into seperate columns
      - [This query](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/blob/main/azure_query) can be used to do that exact thing.
      - As shown below, we have now extracted each field from the RawData

     ![Output From Query](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/e7d9e5a2-8440-4f9d-bd43-cf127ba5399a)
  - Change the `Visualization` from `Set by query` to `Map`
  - Edit the `Map Settings`:

     ![Map Settings](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/b0eca391-b285-49ef-a134-f8158de973f5)
       - Change `Metric Label` to `label`
 
9. **Final Result - Live Attack Map:**
   - Visualize real-time attack data on a world map within Azure Sentinel.
   ![Live Attack Map](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/e8f9ea22-578f-427c-8edb-450fa6369188)
   **Note: This is after approximately 4-6 hours of VM exposure.**

## Acknowledgements

   - I extend my thanks to Josh Madakor for the invaluable guidance provided throughout this exceptional project, which allowed me to gain hands-on experience with Azure Sentinel SIEM. Despite some of the content being out of date, I enjoyed the            challenge of finding my own solutions to create a custom log.
   - The opportunity to explore Azure Sentinel through this project has been immensely educational and I can't wait to truly grasp the power of Sentinel!




