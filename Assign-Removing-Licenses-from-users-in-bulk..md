My [scipt](https://github.com/mattnovitsch/M365/blob/main/Add-RemoveLicenses/Add-RemoveLicenses.ps1) is located here. My script is going to target all users with Flow_Free and remove that then add ATA licenses to those accounts.<BR>
<BR>
**Note:** You will need to change **mattazurelabs:Flow_Free** and **mattazurelabs:ATA** to your organization tenant name and SKUs.<BR>
<BR>
To find your license SKUs, please reference this document: [Product names and service plan identifiers for licensing - Azure AD - Microsoft Entra | Microsoft Learn](https://learn.microsoft.com/en-us/azure/active-directory/enterprise-users/licensing-service-plan-reference)<BR>
<BR>
![image](https://user-images.githubusercontent.com/61195587/215581699-ab7f5b48-6e92-4383-b827-becb88c221e8.png)
<BR>
<#<BR>
#Install Modeule for service<BR>
install-module MSOnline<BR>
<BR>
#Connect to M365 services<BR>
Connect-MsolService<BR>
<BR>
#><BR>
<BR>
#Find your current Account License SKUs<BR>
Get-MsolAccountSku <BR>
<BR>
#Assign location to each user.<BR>
Get-MsolUser -All | where {$_.UsageLocation -eq $null} | Set-MsolUser -UsageLocation US<BR>
<BR>
#Get the users that have the current license you need to swap out.<BR>
$Users = Get-MsolUser -all | Where {$_.Licenses.AccountSkuId -contains "mattazurelabs:Flow_Free"} | Select UserPrincipalName<BR>
<BR>
Foreach ($User in $Users)<BR>
{<BR>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;write-host "Adding mattazurelabs:WIN_DEF_ATP License to uesr:" $User.UserPrincipalName <BR>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set-MsolUserLicense -UserPrincipalName $User.UserPrincipalName -AddLicenses "mattazurelabs:ATA"<BR>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;write-host "Removing mattazurelabs:WIN_DEF_ATP License from uesr:" $User.UserPrincipalName<BR>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set-MsolUserLicense -UserPrincipalName $User.UserPrincipalName -RemoveLicenses "mattazurelabs:Flow_Free"<BR>
} <BR>
 
In my example, I am looking for anyone that has PowerAutomate license and removing it and adding in Defender for Identity. After I run the script you can see there are no users in the Power Automate Free license.<BR>

![image](https://user-images.githubusercontent.com/61195587/215581739-c5cc3727-6b73-417f-9456-40e5522d38a9.png)

