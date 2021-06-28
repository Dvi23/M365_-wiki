**Reference:** <BR>
* [Use Power Automate or Logic Apps to keep an eye on your licenses - JanBakker.tech](https://janbakker.tech/use-power-automate-or-logic-apps-to-keep-an-eye-on-your-licenses/) <BR>
* [Reference guide to using functions in expressions for Azure Logic Apps and Power Automate](https://docs.microsoft.com/en-us/azure/logic-apps/workflow-definition-language-functions-reference) <BR>
* [Power Automate documentation](https://docs.microsoft.com/en-us/power-automate/) <BR>
* [Microsoft Graph REST API v1.0 reference](https://docs.microsoft.com/en-us/graph/api/overview?view=graph-rest-1.0) <BR>
* [Mail Connector - Throttling Limits](https://docs.microsoft.com/en-us/connectors/sendmail/#throttling-limits) <BR>

**Summary** <BR>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; I had a request from a customer to get notifications on when they were running out of licenses. They wanted to know when they were at 90% usage so they could acquire additional licenses or clean up some. I was able to search for a Power Automate report that does this from Jan Bakker from the Netherlands (link in the reference section). I was able to get it setup in my lab in a couple of hours and wanted to create an export for it for easier redistribution and some modifications to what was added to his.<BR>
<BR>
**Prerequisites** <BR>
1. Power Automate Premium subscription.<BR>
2. Download of [License Usage Report](https://github.com/mattnovitsch/M365/blob/main/LicenseUsageReport.zip).<BR>
<BR>

**Steps to install:** <BR>
1.	Login to https://Portal.Azure.com <BR>
2.	Navigate to App Registration <BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365AppRegistration.JPG) 

<BR><BR>
3.	Click On New registration <BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365NewRegistration.JPG) 

<BR><BR>
4.	Give your application a name, I am naming mine License Reporting. You can change who can use the API to whatever option you like and change it later if you desire. Leaving it at default is how I set mine up in my lab. Click Register to complete the application registration process.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365AppRegistration2.JPG)
 
<BR><BR>
5.	Click your application, it should look something like this:<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365ClickApplicaiton.JPG)

<BR><BR> 
6.	We must create a secret for the application (think of it as a token)<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365secret1.JPG)
 
<BR><BR>
7.	Click new client secret.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365secret2.JPG)
 
<BR> <BR>
8.	Add a description and change the expiration date as needed, I put in LicenseReport for the description and left the expiration default.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365secret4.JPG)

<BR> <BR>
9.	Copy the secret value, save it into a notepad or WordPad something where you can retrieve it later. (red square with an arrow pointing to it.)<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365secret3.JPG)
 
<BR><BR>
10.	Navigate to API Permissions on the left.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365API1.JPG)

<BR> <BR>
11.	Click Microsoft Graph.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365API2.JPG)

<BR><BR>
12.	Filter on “organization”. Expand Organization at the bottom and check Organization.Read.All. Click "Update Permissions" to complete.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365API3.JPG)

<BR><BR>
13.	Grant admin consent for your environment.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365API4.JPG)

<BR><BR>
14.	Click on Overview. Copy Client ID and Tenant ID to notepad or WordPad as well.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365IDs.JPG)
<BR><BR>
15.	Navigate to https://us.flow.microsoft.com/ to import the Power Automate workflow.<BR>
16.	Click My flows on the left side.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow1.jpg)

<BR><BR>
17.	Click Import at the top.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow2.jpg)

<BR><BR>
18.	Click Upload.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow3.jpg)

<BR><BR>
19.	Navigate to where you have downloaded Licenseusagereport.zip.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365ImportPackage.JPG)

<BR><BR>
20.	Click the configure wrench (red square) under the Flow resource type. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow4.jpg)

<BR> <BR>
21.	Change the Setup from “update” to “Create as new”. Click save to complete the update to import setup.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow5.jpg)

<BR> <BR>
22.	Click the configure wrench (red square) under the Mail Connection resource type.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow6.jpg)

<BR> <BR>
23.	Click Create New.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow7.jpg)

<BR> <BR>
24.	Click create a connection.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow8.jpg)

<BR><BR>
25.	Type “mail” in the top right corner search box. Then click the + to add the Mail connector.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow9.jpg)

<BR><BR>
26.	Click Accept and create button. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow10.jpg)

<BR><BR>
27.	Close the tab once the Mail connector is created. You should see the Mail Resource on the Import Setup screen now. Click Save to continue.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow11.jpg)

<BR> <BR>
28.	Click import to complete the import process.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow12.jpg)

<BR><BR>
29.	Click Open Flow once the import has successfully imported. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow13.jpg)

<BR> <BR>
30.	You can change the recurrence from 1 day to whatever you desire. This is done by selecting the Recurrence action on the top of the flow.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow17.jpg)

<BR> <BR>
31.	Get your notepad or WordPad ready, this is where we need those IDs. Open the HTTP action, click on “Show advance Options”.  Replace the word TenantID with your TenantID number, ClientID with your client number, and SecretPassword with your Secret password. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow19.jpg)

<BR> <BR>
32.	Change the condition to meet your company’s requirements. Right now, its setup for 10% so I could trigger it in my lab. If you want daily emails, then 10% would be fine. If you want to know when you are 75% then just change it to 75. Scroll down to Apply to each > Condition then change the 10 to your desire configuration. You could also delete percentage and use totals also, that would be completely up to your company. This template is just for percentage.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow14.jpg)

<BR><BR>
33.	The last thing we need to change is the email address this is going to. Right now, its setup to go to Testing@reply.com. You will need to change it to a distribution list or person(s) you want to get this notification. Please note that there limits to the number of emails that can be sent. [Mail Connector - Throttling Limits](https://docs.microsoft.com/en-us/connectors/sendmail/#throttling-limits)<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow18.jpg)

<BR><BR>
34.	Please remember to Save it. Top right corner. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow15.jpg)

<BR><BR>
35.	Click “Turn on” in the action bar. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365Flow16.jpg)

<BR><BR>
**NOTE:** Due to replication between the AAD and Power Automate permissions for the API could take several hours to complete. You might see errors that say you have insufficient privileges. <BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365Error.jpg)

<BR> 
36.	Once complete you should start getting emails like this: <BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365Email.jpg)

<BR><BR>