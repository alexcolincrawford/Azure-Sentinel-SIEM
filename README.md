#  Azure-Sentinel-SIEM

I always wondered how I could gain hands-on experience with a powerful SIEM like Azure Sentinel, but finding the right resources seemed impossible. Now, I'm determined to make it happen by setting up my own Azure Sentinel homelab, using the free $200 credit to maximize my hands-on experience and learn the ins and outs of this powerful tool.

This project creates an exposed virtual machine that relays the failed RDP attempts to Azure Sentinel.



### Steps

**Note: This Project Requires A Microsoft Azure Subscription!**

1. **Creating Honeypot Virtual Machine:**
   _Fill out the relevant information..._
   
   1. Create a new resource group! I named mine 'honeypot'.
   2. GIve it an appropriate name! I named mine 'honeypot-vm'.
   3. Select an appropriate region
   4. Select Win11 Pro for the OS.
  
![image](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/5cbff611-e487-4702-8596-0df13c723adb)

   - **Note: **Ensure that a strong password is allocated to the virtual machine, as it will exposed.
   - When it comes to `size`, I went with the cheapest, available one that supported 8GiB of RAM.
     
   ![image](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/3c8f56c7-7485-4231-b652-942da272de51)
   
2. **Creating Log Analytics Workspace:**
   - Create 


