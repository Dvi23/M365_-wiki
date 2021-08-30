# Summary
Turn on Azure AD Logs for reporting data.

## Steps
1. Log into [Azure Portal](https://portal.azure.com)
2. Search for "Azure Active Directory" in the top bar, the click on Azure Active Directory. 
![](https://github.com/mattnovitsch/M365/blob/main/AADLogs1.jpg)
3. On the left side panel, look for Monitoring and then click on Diagnostic Settings. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/AADLogs2.jpg)
4. Click +Add diagnostic settings. 
5. Select all the logs then select a location for the logs, in this example we are using Log Analytics workspace. Provide a name for the logs also, I used All Azure AD Logs.
* Note: The Signin logs require AAD P1 or P2.
![](https://github.com/mattnovitsch/M365/blob/main/AADLogs3.jpg)
6. Select Log Analytics under monitoring on the left. Under LogManagement double click SigninLogs. Make sure to change the Time range to Last 7 days. Click Export then Export to Power BI (M query).
![](https://github.com/mattnovitsch/M365/blob/main/AADLogs4.jpg) 
7. Ease SigninLogs and double click on AADNonInteractiveUserSigninLogs, then click Export then Export to Power BI (M query).
![](https://github.com/mattnovitsch/M365/blob/main/AADLogs5.jpg) 
8. The PowerBIQuery.txt files can be used at anytime in the creation of the dashboard going forward, it is used in the [Microsoft Defender for Endpoint Dashboard](https://github.com/mattnovitsch/M365/wiki/Microsoft-Defender-for-Endpoint-Dashboard). 