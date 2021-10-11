# Summary:
<BR>
This report is meant to give you a general overview of your licenses and breakdowns of each user. This is uses the Graph APIs then stores the data into Azure Log Analytics. Cost for Azure Log Analytics will vary depending on your organizations size. This took me awhile since I last build the License Overview that required a global administrator to run the PowerShell scripts daily. I didn't like the fact that was a requirement and started looking into Graph. After many failed attempts and a support case to help me with some JSON issues I finally got it working.<BR>
<BR> Please note I am not a licensing expert by any means. What I have found that in creating this report, Microsoft Licensing is really confusing to me so I have given it my best effort. An example of this is, if you turn off Microsoft Insider Risk Management it shows up in the report as Exchange as part of that component so you will see Exchange enable and disabled because of piece of Exchange(Microsoft Insider Risk Management module) is disabled.


## Prerequisites: <br>

* Power Automate Premium License
* [PowerBI Desktop x64](https://www.microsoft.com/en-us/download/details.aspx?id=58494) or [Power BI Report Server](https://powerbi.microsoft.com/en-us/report-server/)
* [M365Dashboard.pbit](https://github.com/mattnovitsch/M365/blob/main/M365Dashboard.pbit)
* [PowerBI-AssignedLicense](https://github.com/mattnovitsch/M365/blob/main/PowerBI-AssignedLicense_20211011134926.zip)
* [PowerBI-LicenseReport](https://github.com/mattnovitsch/M365/blob/main/PowerBI-LicenseReport_20211011135031.zip)
* [PowerBI-assignedPlans](https://github.com/mattnovitsch/M365/blob/main/PowerBI-assignedPlans_20211011135001.zip)
<BR>

## References:

* [Product names and service plan identifiers for licensing](https://docs.microsoft.com/en-us/azure/active-directory/enterprise-users/licensing-service-plan-reference)
* [Permissions and consent in the Microsoft identity platform - Permission types](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-permissions-and-consent?WT.mc_id=Portal-Microsoft_AAD_RegisteredApps#permission-types)
<BR>

## Steps: <BR>

1. Navigate to [Power Automate](https://flow.microsoft.com)
2. Click on My Flows then Import.
![](https://github.com/mattnovitsch/M365/tree/main/M365License/M365L1.jpg)
3. Click Upload.
![](https://github.com/mattnovitsch/M365/tree/main/M365License/M365L2.jpg)
4. Navigate where you downloaded [PowerBI-AssignedLicense](https://github.com/mattnovitsch/M365/blob/main/PowerBI-AssignedLicense_20211009122143.zip),  [PowerBI-LicenseReport](https://github.com/mattnovitsch/M365/blob/main/PowerBI-LicenseReport_20211009122547.zip), and [PowerBI-assignedPlans](https://github.com/mattnovitsch/M365/blob/main/PowerBI-assignedPlans_20211009121621.zip). Select one of the files then click open.
![](https://github.com/mattnovitsch/M365/tree/main/M365License/M365L3.jpg)
5. Once the Package has uploaded you will need the review process, this is required to correct the configurations of the package. Click the Action wrench to configure each area.
![](https://github.com/mattnovitsch/M365/tree/main/M365License/M365L4.jpg)
6. In this example our first configuration item is the option to update or create as new, this is because my lab already has the package. This will be handy if I ever need to update it and repost for everyone to use. I'm going to create as new in this example and add the tag -demo on the resource name. Yours should be just create as new or it will probably not ask you at all. I'm clicking save to proceed.
![](https://github.com/mattnovitsch/M365/tree/main/M365License/M365L5.jpg)
7. If you do not have a Azure Log Analytics connection then click create new. If you do have one, select your existing connection and click save.
![](https://github.com/mattnovitsch/M365/tree/main/M365License/M365L6.jpg)
8. Skip steps 8 through 10 if you already have a connection. Click New Connection in the top of the new tab.
![](https://github.com/mattnovitsch/M365/tree/main/M365License/M365L7.jpg)
9. Type Azure Log in the top right Search box and then select Azure Log Analytics Data Collector.
![](https://github.com/mattnovitsch/M365/tree/main/M365License/M365L8.jpg)
10. Type in your Workspace ID and Workspace Key. (You can get your keys by following these steps: [Getting Azure Log Analytics Keys](https://github.com/mattnovitsch/M365/wiki/Getting-Azure-Log-Analytics-Keys))
11. Once you save the connection Navigate back to the Flow screen and hit refresh. Select Azure Log Analytics then click Save.
![](https://github.com/mattnovitsch/M365/tree/main/M365License/M365L9.jpg)
12. Now that the configurations are complete, you can click import. Do this for the remaining two Flows that you downloaded from [Prerequisites](https://github.com/mattnovitsch/M365/wiki/M365-Licensing-Overview---In-Progress/_edit#prerequisites-)
![](https://github.com/mattnovitsch/M365/tree/main/M365License/M365L10.jpg)
13. One all three flows are in the system, select one.
![](https://github.com/mattnovitsch/M365/tree/main/M365License/M365L11.jpg)
14. Click Edit in the top middle part of the screen.
![](https://github.com/mattnovitsch/M365/tree/main/M365License/M365L12.jpg)
15. Click HTTP then click Show Advanced Options.
![](https://github.com/mattnovitsch/M365/tree/main/M365License/M365L13.jpg)
16. Go down Tenant, Client ID, and Secret. (If you don't know this information please refer too [Register a New application](https://github.com/mattnovitsch/M365/wiki/Register-a-New-application)
![](https://github.com/mattnovitsch/M365/tree/main/M365License/M365L14.jpg)