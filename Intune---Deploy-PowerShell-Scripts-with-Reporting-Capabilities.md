# Summary

Deploying Custom Inventory PowerShell scripts via Intune. We will walk through deploying the custominventory script and how to get reporting data off of it. Most of the script came from Jan Ketil Skanke but I modified it to add some additional security settings I was looking for on the devices.

## Reference
* [Enhance Intune Inventory Data with Proactive Remediations and Log Analytics](https://msendpointmgr.com/2021/04/12/enhance-intune-inventory-data-with-proactive-remediations-and-log-analytics/)

## Prerequisites
* [CustomInventory.ps1](https://github.com/mattnovitsch/M365/blob/main/CustomInventory.ps1)
* Active Azure Subscription
* Deployed Log Analytics environment

## Steps

1. Navigate to [Azure Portal](https://portal.azure.com/#allservices).
2. Select Analytics on the left side then select Log Analytics Workspaces.
![](https://github.com/mattnovitsch/M365/blob/main/UC2.jpg) 
3. Select your workspace, then select Agents Management. Copy the Workspace ID and Primary Key to a notepad.
![](https://github.com/mattnovitsch/M365/blob/main/DPS1.jpg)
3. Download [CustomInventory.ps1](https://github.com/mattnovitsch/M365/blob/main/CustomInventory.ps1)
4. Open CustomInventory.ps1 in PowerShell ISE as an administrator.
5. Go to line 25 where it has $CustomerID = "", paste your customer ID there. Past your Primary Key on line 28: $SharedKey = ""
![](https://github.com/mattnovitsch/M365/blob/main/DPS2.jpg)
6. Save CustomInventory.ps1
7. Navigate to [Intune](https://endpoint.microsoft.com)
8. Navigate to Devices > Scripts then click Add then select Windows 10.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/DPS3.jpg)
9. Enter a name for the script. I am using Custom_Inventory for this example, click Next to continue.
![](https://github.com/mattnovitsch/M365/blob/main/DPS4.jpg)
10. Browse to the location where CustomInventory.ps1 and select it. Also make sure to set "Run script in 64 bit PowerShell Host" to Yes. Click Next to continue.
![](https://github.com/mattnovitsch/M365/blob/main/DPS5.jpg)
11. Add a test group(s) that you want to include and any that you want to exclude, then click Next.
![](https://github.com/mattnovitsch/M365/blob/main/DPS6.jpg)
12. Review the configuration and click Add to finish deployment of the script. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/DPS7.jpg)

# Note
Please give this a couple of hours before trying to pull data, it could take longer depending on your environment size. You can validate there is data by navigating back to Log Analytics Workspace > "YourWorkplace" > Logs. You should see Custom Logs AppInventory_CL and DeviceInventory_CL. 
![](https://github.com/mattnovitsch/M365/blob/main/DPS8.jpg)