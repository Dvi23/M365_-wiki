**Summary:** <BR>
<BR>
This report is meant to give you a general overview of your licenses and breakdowns of each user. It doesn't have to be ran in Power BI Online and the data needs to be retrieved from the Global Administrator. <BR>

**NOTE: It is not automated for security reasons.**<BR>

Prerequisites
* [LicensingPowerBI.ps1](https://github.com/mattnovitsch/M365/blob/main/LicensingPowerBI.ps1)
* [PowerBI Desktop x64](https://www.microsoft.com/en-us/download/details.aspx?id=58494) or [Power BI Report Server](https://powerbi.microsoft.com/en-us/report-server/)
* [LicensingOverview.pbit](https://github.com/mattnovitsch/M365/blob/main/LicensingOverview.pbit)

<BR>

**Steps:**<BR>
<BR>

1. Open PowerShell ISE as an administrator.<BR>
<BR>

2. Navigate to where you downloaded LicensingPowerBI.ps1 and open it.<BR>
<BR>

3. Scroll down to the bottom of the ps1 file where you see export-csv -path c:\data.csv. Change the path to your desired location. Feel free to change the file names as well, these will be changed in the Power BI application later. I have it set to the root of my C drive, but if you want others to view the report you can place it on a network share. You will need to do this for lines 58 and 60.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview1.JPG)

<BR>

4. Highlight lines 1 through 17, then click the “Run Selection” button or press F8.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview2.JPG)

<BR>

5. If you have the modules installed, please skip to step 8. If not, please keep reading. You will be prompted to install NuGet Provider, click yes to continue.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview3.JPG)

<BR>

6. Click Yes to all to install the Azure AD module.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview4.JPG)

<BR>

7. You will then be prompted to install MSOService module, click Yes to all for that one as well.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview4.JPG)

<BR>

8. Highlight lines 19 through 27, then click the “Run Selection” button or press F8.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview5.JPG)

<BR>

9. You will be prompted to sign into your tenant, follow the prompts that appear.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview6.JPG)

<BR> 

10. Highlight line 35, then click the “Run Selection” button or press F8.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview7.JPG)

<BR>

11. You will be prompted to sign into your tenant, follow the prompts that appear again.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview6.JPG)

<BR>

12. Now that we have the modules installed and the connections to Azure connected run the entire script by pressing the green play button or pressing F5

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview19.JPG)

<BR>

13.  To confirm that it worked successfully, you should see modules exist and still connected to M365 and AzureAD in PowerShell ISE and two files where you set the locations at in step 3.  
<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview8.JPG)
![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview9.JPG)
<BR>

14. Open LicensingOverview.pbit.<BR>

<BR>

15. If you changed the file name and/or location you will get error stating “Could not find file ‘C:\Data2.csv’.” If you did not change the names or path then skip to step 23. Close the error message.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview10.JPG)

<BR>

16. Right click on LicnseNumbers in the fields column on the right and select Edit query.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview11.JPG)

<BR> 

17. Right click on Source in the Query Settings on the right then select Edit Settings.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview12.JPG)

<BR>

18. Change the File path and name to whatever you defined in step 3(line 60 in the PowerShell). Click Ok when done.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview13.JPG)

<BR>

19. Click LicenseOverview on the left side of the screen.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview14.JPG)

<BR>  

20. Right click on Source in the Query Settings on the right then select Edit Settings.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview12.JPG)

<BR>

21. Change the File path and name to whatever you defined in step 3(line 58 in the PowerShell). Click Ok when done.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview15.JPG)

<BR>

22. Click Close & Apply in the top right corner of the screen to save the setting.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview16.JPG)

<BR>

23. The screen should refresh and you should see something like this.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview17.JPG)
![](https://github.com/mattnovitsch/M365/blob/main/M365LicensingOverview18.JPG)

<BR>
<BR>