# Update 9/7/2021
I found out the column I was user for what I thought was primary user was in fact enrollment user. I had to add another table called userDeviceAssociations and redo some of the relationships on the tables but I got it corrected now. Please download the new [MEM Dashboard](https://github.com/mattnovitsch/M365/blob/main/MEMDashboard.pbit) file to get the corrections.

# Summary
This will Power BI report has the following information in it:
* Device usage
* Updates Compliance
* Hardware Inventory
* Application Inventory
* Endpoint Security

![](https://github.com/mattnovitsch/M365/blob/main/Dashboard1.jpg)
![](https://github.com/mattnovitsch/M365/blob/main/Dashboard2.jpg)
![](https://github.com/mattnovitsch/M365/blob/main/Dashboard3.jpg)
![](https://github.com/mattnovitsch/M365/blob/main/Dashboard4.jpg)
![](https://github.com/mattnovitsch/M365/blob/main/Dashboard6.jpg)

## Prerequisites
* [PowerBI Desktop x64](https://www.microsoft.com/en-us/download/details.aspx?id=58494) or [Power BI Report Server](https://powerbi.microsoft.com/en-us/report-server/)
* [MEM Dashboard](https://github.com/mattnovitsch/M365/blob/main/MEMDashboard.pbit)
* [Update Compliance Enabled](https://github.com/mattnovitsch/M365/wiki/Enabling-Update-Compliance)
* [How to retrieve your Intune Data Warehouse URL](https://github.com/mattnovitsch/M365/wiki/How-to-retrieve-your-Intune-Data-Warehouse-URL)
* [Intune Deploy PowerShell Scripts with Reporting Capabilities](https://github.com/mattnovitsch/M365/wiki/Intune---Deploy-PowerShell-Scripts-with-Reporting-Capabilities)
* Power BI Pro License (if you want to publish for others in your organization to see)

## Steps
1. Open [MEM Dashboard](https://github.com/mattnovitsch/M365/blob/main/MEMDashboard.pbit)
2. You will be prompted to login after it tries to retrieve data from my environment which it will fail. Click Cancel. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/UCD1.jpg)

3. Click close on the refresh screen.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/UCD2.jpg)

4. Right click on Devices on the right hand side and select Edit query.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/UCD3.jpg)

5. Right click on Source and select Edit Settings. On the OData Feed, change the URL to the [data warehouse](https://github.com/mattnovitsch/M365/wiki/How-to-retrieve-your-Intune-Data-Warehouse-URL) URL that should be in your notepad.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/UCD4.jpg)
<BR>
6. Click Organizational account, then click Sign in. <BR>

![](https://github.com/mattnovitsch/M365/blob/main/UCD5.jpg)
<BR>
7. Follow any prompts to login to your M365 account, chances are if you are already logged it then you can just click connect. <BR>

![](https://github.com/mattnovitsch/M365/blob/main/UCD6.jpg)
<BR>
8. Repeat this step for all the tables except for UpdateDeployment, AppInventory, and DeviceInventory.

![](https://github.com/mattnovitsch/M365/blob/main/UCD7.jpg)
<BR>

9. Navigate to the [Azure Portal](https://portal.azure.com/#allservices)
10. Select Analytics on the left side then select Log Analytics Workspaces.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/UC2.jpg)
11. Select your workspace, then select Solutions. Select WaaSUpdateInsights.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/UC3.jpg)
12. Select Update Compliance window.
![](https://github.com/mattnovitsch/M365/blob/main/UCD8.jpg)
13. Select Logs. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/UCD9.jpg)
14. Change the time range to 7 days and type in "WaaSDeploymentStatus" in the query field. Click Run to execute the query.
![](https://github.com/mattnovitsch/M365/blob/main/UCD10.jpg)
15. Select Export and Export to Power BI(M query)
![](https://github.com/mattnovitsch/M365/blob/main/UCD11.jpg)
16. Open the PowerBIQuery.txt file that gets downloaded. Copy all the contents inside it.
17. Go back to Power BI and left click on UpdateDeployment then select Advance Editor.
![](https://github.com/mattnovitsch/M365/blob/main/UCD12.jpg)
18. Delete all the content that is in the UpdateDeployment Advance Editor screen and paste in what you got from the PowerBIQuery.txt file that you downloaded from step above. Click done to save the update. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/UCD13.jpg)
19. Click Close & Apply in the top right corner. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/UCD14.jpg)
20. Wait for the report to collect the data. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/UCD15.jpg)

You have completed the deployment of the dashboard, don't forget to save it. Your dashboards should look something like these.
![](https://github.com/mattnovitsch/M365/blob/main/Dashboard1.jpg)
![](https://github.com/mattnovitsch/M365/blob/main/Dashboard2.jpg)
![](https://github.com/mattnovitsch/M365/blob/main/Dashboard3.jpg)
![](https://github.com/mattnovitsch/M365/blob/main/Dashboard4.jpg)
![](https://github.com/mattnovitsch/M365/blob/main/Dashboard6.jpg)
