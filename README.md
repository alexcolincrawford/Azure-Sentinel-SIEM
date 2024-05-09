#  Azure-Sentinel-SIEM

I always wondered how I could gain hands-on experience with a powerful SIEM like Azure Sentinel, but finding the right resources seemed impossible. Now, I'm determined to make it happen by setting up my own Azure Sentinel homelab, using the free $200 credit to maximize my hands-on experience and learn the ins and outs of this powerful tool.

This project creates an exposed virtual machine that relays the failed RDP attempts to Azure Sentinel.



### Steps

**Note: This Project Requires A Microsoft Azure Subscription!**

1. **Creating Honeypot Virtual Machine:**
   - Fill out the relevant information...
  
  ![image](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/97940d29-5697-49f6-bf51-2307b1dce28f)
  
   - Ensure that a strong password is allocated to the virtual machine, as it will exposed.
     
   ![image](https://github.com/alexcolincrawford/Azure-Sentinel-SIEM/assets/59071533/3c8f56c7-7485-4231-b652-942da272de51)
   - When it comes to `size`, I went with the cheapest, available one that supported 8GiB of RAM.

2. **Creating Log Analytics Workspace:**
   - Create 


