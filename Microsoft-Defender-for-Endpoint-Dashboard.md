# Summary
I’ve been working with Microsoft Defender for Endpoints for about a month with my customers as it has suddenly been a very hot topic for them. Since I have only read about it and not had any hands on experience I figured it was time to throw it up in my lab. It was deployed, great now what? I then started to pull data from the API and created several pages off the system. This dashboard will provide you with your endpoint health status in the security portal, provide you with CVE vulnerabilities, and provide you with details on threats per endpoint. This information is pulled directly from the Microsoft Security API for your tenant.  The pages include:

* ATP-Overview
* ATP- Application Inventory
* CVEVulnerabilities
* ATP - Hunting
* ATP - Unhealthy Endpoints
* ATP - High Risk Endpoints

## Prerequisites
* PowerBI Desktop x64 or Power BI Report Server
* [MDE Dashboard](https://github.com/mattnovitsch/M365/tree/main/MDE/MDEDashboard.pbit)
* [Turn on Diagnostic Settings(optional)](https://github.com/mattnovitsch/M365/wiki/Turn-on-Azure-AD-logs) 

## Steps
1. Open [MDE Dashboard](https://github.com/mattnovitsch/M365/blob/main/MDEDashboard.pbit). <BR>
**Note: This will take a few minutes as its building the local database to generate the dashboards.**
2. Select any data set from the Fields column on the right and select Edit Query. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/MDE/MDE1.jpg) 
3. Click AADSignons on the left hand side where it says Queries then select Advance Editor at the top. 
![](https://github.com/mattnovitsch/M365/blob/main/MDE/MDE2.jpg) 
4. Open the first PowerBIQuery.txt file you saved from the [Azure AD Signon Logs.](https://github.com/mattnovitsch/M365/wiki/Turn-on-Azure-AD-logs). 
5. Copy all the content and paste it in the Advance Editor then click done.
* Note:  there is a GUID that changes per workspace in here.
![](https://github.com/mattnovitsch/M365/blob/main/MDE/MDE3.jpg) 
6. Click AADSignon-Noninteractive on the left hand side where it says Queries then select Advance Editor at the top. 
7. Open the second PowerBIQuery.txt file you saved from the [Azure AD Signon Logs.](https://github.com/mattnovitsch/M365/wiki/Turn-on-Azure-AD-logs). 
8. Copy all the content and paste it in the Advance Editor then click done.
* Note:  there is a GUID that changes per workspace in here.
![](https://github.com/mattnovitsch/M365/blob/main/MDE/MDE4.jpg) 
9. Click Close & Apply when finished. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/MDE/MDE5.jpg) 

Once the data has been refreshed you should see something like these. <BR> 
* Note: There is a unhealthy Endpoint page that I was not able to populate due to the fact that it requires loading viruses and malware on the system and I'm sure Microsoft Security wouldn't like that much.

![](https://github.com/mattnovitsch/M365/blob/main/MDE/MDED1.jpg)<br>
![](https://github.com/mattnovitsch/M365/blob/main/MDE/MDED2.jpg)<br>
![](https://github.com/mattnovitsch/M365/blob/main/MDE/MDED3.jpg)<br>
![](https://github.com/mattnovitsch/M365/blob/main/MDE/MDED4.jpg)<br>
![](https://github.com/mattnovitsch/M365/blob/main/MDE/MDED5.jpg)<br>
![](https://github.com/mattnovitsch/M365/blob/main/MDE/MDED6.jpg)<br>
![](https://github.com/mattnovitsch/M365/blob/main/MDE/MDED7.jpg)<br>
 