# Summary
Register an application for API calls with applications like Power BI and Power Automate.

## Prerequisites
* Azure subscription

## Steps
1. Log into [Azure Portal](https://portal.azure.com/#allservices).
2. In the search box, type in Active Directory then click Azure Active Directory. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/ApplicationRegistration/AP1.jpg)
3. Select App Registrations on the left hand menu, then select New Registration.  <BR>
![](https://github.com/mattnovitsch/M365/blob/main/ApplicationRegistration/AP2.jpg)
4. Give the application a name. I'm going to call mine "Demo Application". Fill in who can access the API and if you require a redirection URI. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/ApplicationRegistration/AP3.jpg)
5. Copy the Application (client) ID and Directory (tenant) ID for later use. I do notepad on the desktop without saving it. Click 
Add a certificate or secret.  <BR>
![](https://github.com/mattnovitsch/M365/blob/main/ApplicationRegistration/AP4.jpg)
6. Click New Client Secret.  <BR>
![](https://github.com/mattnovitsch/M365/blob/main/ApplicationRegistration/AP5.jpg)
7. Enter the description and select the timeframe you want the secret to be valid for. You might want to check with your Cyber team to figure out your organizational requirements.  <BR>
![](https://github.com/mattnovitsch/M365/blob/main/ApplicationRegistration/AP6.jpg)
8. Click the copy icon and save the secret in the notepad for later use. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/ApplicationRegistration/AP7.jpg)