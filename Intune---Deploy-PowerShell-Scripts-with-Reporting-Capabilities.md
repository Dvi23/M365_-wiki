# Summary

Deploying Custom Inventory PowerShell scripts via Intune. We will walk through deploying the custominventory script and how to get reporting data off of it. Most of the script came from Jan Ketil Skanke but I modified it to add some additional security settings I was looking for on the devices.

# Major Update - 8/9/2021

The scripts need to be deployed under Endpoint Analytics so they are continuously ran, the scripts only run once until successful otherwise.

## Reference
* [Enhance Intune Inventory Data with Proactive Remediations and Log Analytics](https://msendpointmgr.com/2021/04/12/enhance-intune-inventory-data-with-proactive-remediations-and-log-analytics/)

## Prerequisites
* [CustomInventory.ps1](https://github.com/mattnovitsch/M365/blob/main/CustomInventory.ps1)
* Active Azure Subscription
* Deployed Log Analytics environment

## Steps

1. Navigate to [Azure Portal](https://portal.azure.com/#allservices).
2. Select Analytics on the left side then select Log Analytics Workspaces.
![](https://github.com/mattnovitsch/M365/blob/main/UpdateCompliance/UC2.jpg) 
3. Select your workspace, then select Agents Management. Copy the Workspace ID and Primary Key to a notepad.
![](https://github.com/mattnovitsch/M365/blob/main/DeployPowerShellScriptMEM/DPS1.jpg)
3. Download [CustomInventory.ps1](https://github.com/mattnovitsch/M365/blob/main/CustomInventory.ps1)
4. Open CustomInventory.ps1 in PowerShell ISE as an administrator.
5. Go to line 25 where it has $CustomerID = "", paste your customer ID there. Past your Primary Key on line 28: $SharedKey = ""
![](https://github.com/mattnovitsch/M365/blob/main/DeployPowerShellScriptMEM/DPS2.jpg)
6. Save CustomInventory.ps1
7. Navigate to [Microsoft Endpoint Manager](https://endpoint.microsoft.com)
8. Navigate to Reports > Endpoint Analytics.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/DeployPowerShellScriptMEM/DPS3.jpg)
9. Click on Proactive remediations > Create Script Package.
![](https://github.com/mattnovitsch/M365/blob/main/DeployPowerShellScriptMEM/DPS4.jpg)
10. Provide the script a name, for example CustomInventory then click Next.
![](https://github.com/mattnovitsch/M365/blob/main/DeployPowerShellScriptMEM/DPS5.jpg)
11. Upload your customerinventory.ps1 script and make sure Run Script as 64-Bit is set to yes, then click Next.
![](https://github.com/mattnovitsch/M365/blob/main/DeployPowerShellScriptMEM/DPS6.jpg)
12. Assign any Scope Tags then click next.
13. Assign the groups you want the scripts to deploy to, I'm deploying to all devices for this example. Change the schedule to your desire, daily is fine. Click next to continue.
![](https://github.com/mattnovitsch/M365/blob/main/DeployPowerShellScriptMEM/DPS7.jpg)
14. Review your remediation for errors then click create to complete the setup.
![](https://github.com/mattnovitsch/M365/blob/main/DeployPowerShellScriptMEM/DPS8.jpg)

# Note
Please give this a couple of hours before trying to pull data, it could take longer depending on your environment size. You can validate there is data by navigating back to Log Analytics Workspace > "YourWorkplace" > Logs. You should see Custom Logs AppInventory_CL and DeviceInventory_CL. 
![](https://github.com/mattnovitsch/M365/blob/main/DPS9.jpg)