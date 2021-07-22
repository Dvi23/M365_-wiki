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
5. Go to line 25 where it has $CustomerID = ""
4. Paste your customer ID in there.