# Summary:
<BR>
This report is meant to give you a general overview of your licenses and breakdowns of each user. This is uses the Graph APIs then stores the data into Azure Log Analytics. Cost for Azure Log Analytics will vary depending on your organizations size. This took me awhile since I last build the License Overview that required a global administrator to run the PowerShell scripts daily. I didn't like the fact that was a requirement and started looking into Graph. After many failed attempts and a support case to help me with some JSON issues I finally got it working.<BR>
<BR> Please note I am not a licensing expert by any means. What I have found that in creating this report, Microsoft Licensing is really confusing to me so I have given it my best effort. An example of this is, if you turn off Microsoft Insider Risk Management it shows up in the report as Exchange as part of that component so you will see Exchange enable and disabled because of piece of Exchange(Microsoft Insider Risk Management module) is disabled.


# Prerequisites: <br>
* Power Automate Premium License
* [PowerBI Desktop x64](https://www.microsoft.com/en-us/download/details.aspx?id=58494) or [Power BI Report Server](https://powerbi.microsoft.com/en-us/report-server/)
* [M365License.pbit](https://github.com/mattnovitsch/M365/blob/main/M365License.pbit)
* [PowerBI-AssignedLicense](https://github.com/mattnovitsch/M365/blob/main/PowerBI-AssignedLicense_20211009122143.zip)
* [PowerBI-LicenseReport](https://github.com/mattnovitsch/M365/blob/main/PowerBI-LicenseReport_20211009122547.zip)
* [PowerBI-assignedPlans](https://github.com/mattnovitsch/M365/blob/main/PowerBI-assignedPlans_20211009121621.zip)
<BR>

# References:
* [Product names and service plan identifiers for licensing](https://docs.microsoft.com/en-us/azure/active-directory/enterprise-users/licensing-service-plan-reference)
* [Permissions and consent in the Microsoft identity platform - Permission types](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-permissions-and-consent?WT.mc_id=Portal-Microsoft_AAD_RegisteredApps#permission-types)
<BR>