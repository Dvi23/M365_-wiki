# Summary
This will walk you through enabling Update Compliance on your endpoints and M365 tenant.

## Prerequisites
* Active Azure Subscription (I used a free one in my lab)

## References
* [Get started with Update Compliance](https://docs.microsoft.com/en-us/windows/deployment/update/update-compliance-get-started)
* [Configuring devices through the Update Compliance Configuration Script](https://docs.microsoft.com/en-us/windows/deployment/update/update-compliance-configuration-script)
* [Manually Configuring Devices for Update Compliance](https://docs.microsoft.com/en-us/windows/deployment/update/update-compliance-configuration-manual)

## Steps
1. Navigate to [Azure Marketplace](https://azuremarketplace.microsoft.com/en-US/marketplace/apps/microsoft.waasupdateinsights?tab=overview) (Make sure you are logged into your Azure subscription).
2. Click Get it now.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/UC1.jpg)
3. Choose an existing or configure a new Log Analytics Workspace, ensuring it is in a Compatible Log Analytics region from the following [table](https://docs.microsoft.com/en-us/windows/deployment/update/update-compliance-get-started#add-update-compliance-to-your-azure-subscription).  Although an Azure subscription is required, you won't be charged for ingestion of Update Compliance data.
* Desktop Analytics users should use the same workspace for Update Compliance.
* Azure Update Management users should use the same workspace for Update Compliance.
4. Once deployed, navigate to [Azure Portal](https://portal.azure.com/#allservices).
5. Select Analytics on the left side then select Log Analytics Workspaces.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/UC2.jpg)
6. Select your workspace, then select Solutions. Select WaaSUpdateInsights, if you do not see WaaSUpdateInsights, check to see that your deployment for Azure Marketplace was successful.<BR>
![](https://github.com/mattnovitsch/M365/blob/main/UC3.jpg)
7. Select Update Compliance Setting, then click the copy icon (you will need to save this for later, copying to a notepad would be helpful).<BR>
![](https://github.com/mattnovitsch/M365/blob/main/UC4.jpg)
<BR><BR>
There are 3 different ways to [Enroll devices in Update Compliance](https://docs.microsoft.com/en-us/windows/deployment/update/update-compliance-get-started#enroll-devices-in-update-compliance). I have done them all, but the [Microsoft Endpoint Manager](https://docs.microsoft.com/en-us/windows/deployment/update/update-compliance-configuration-mem) one is the easiest long term to support. I found to get my data enter in I had to do the script and MEM configuration policy for it to work correctly. We will be walking through the MEM and script option here. Navigate to 
8. Navigate to the [Microsoft Endpoint Management Admin Center](https://endpoint.microsoft.com/#blade/Microsoft_Intune_DeviceSettings/DevicesWindowsMenu/configProfiles) >Devices > Windows > Configuration Profiles.
9. Click New Profile. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/UC5.jpg) 
10. Select the following: 
* Windows 10 and Later for the platform. 
* Templates on the profile type.
* Custom for the Template Name.
* Select Create to start configure the policy.
<BR>

![](https://github.com/mattnovitsch/M365/blob/main/UC6.jpg) 

<BR>
11. Provide your policy a name, I did Update Compliance Settings. Click Next once complete<BR>

![](https://github.com/mattnovitsch/M365/blob/main/UC7.jpg) 

<BR>
13. You will be adding multiple OMA-URI Settings that correspond to the policies described in Manually configuring devices for Update Compliance. Click Add on the Configuration Settings Screen to start adding the settings. <BR>

![](https://github.com/mattnovitsch/M365/blob/main/UC8.jpg)

<BR>
14. Add the following settings then click save: <BR>
* Name: Commercial ID <BR>
* Description: Sets the Commercial ID that corresponds to the Update Compliance Log Analytics workspace. <BR>
* OMA-URI: ./Vendor/MSFT/DMClient/Provider/ProviderID/CommercialID <BR>
* Data type: String <BR>
* Value: "enter your CommericalID from the notepad you saved it on earlier"<BR>

![](https://github.com/mattnovitsch/M365/blob/main/UC9.jpg)

<BR>
15. Click Add on the Configuration Settings Screen to start add the next settings. <BR>
16. Add the following settings then click save: <BR>
* Name: Allow Telemetry <BR>
* Description: Sets the maximum allowed diagnostic data to be sent to Microsoft, required for Update Compliance. <BR>
* OMA-URI: ./Vendor/MSFT/Policy/Config/System/AllowTelemetry <BR>
* Data type: Integer <BR>
* Value: 1 (all that is required is 1, but it can be safely set to a higher value). I changed mine to 3 for optional. <BR>

![](https://github.com/mattnovitsch/M365/blob/main/UC10.jpg)

<BR>
17. Click Add on the Configuration Settings Screen to start add the next settings. <BR>
18. Add the following settings then click save: <BR>
* Name: Disable Telemetry opt-in interface <BR>
* Description: Disables the ability for end-users of devices can adjust diagnostic data to levels lower than defined by the Allow Telemetry setting. <BR>
* OMA-URI: ./Vendor/MSFT/Policy/Config/System/ConfigureTelemetryOptInSettingsUx <BR>
* Data type: Integer <BR>
* Value: 1 <BR>

![](https://github.com/mattnovitsch/M365/blob/main/UC12.jpg)

<BR>
17. Click Add on the Configuration Settings Screen to start add the next settings. <BR>
18. Add the following settings then click save: <BR>
* Name: Allow device name in Diagnostic Data <BR>
* Description: Allows device name in Diagnostic Data. <BR>
* OMA-URI: ./Vendor/MSFT/Policy/Config/System/AllowDeviceNameInDiagnosticData <BR>
* Data type: Integer <BR>
* Value: 1 <BR>

![](https://github.com/mattnovitsch/M365/blob/main/UC13.jpg)

<BR>
19. Click Add on the Configuration Settings Screen to start add the next settings. <BR>
20. Add the following settings then click save: <BR>
* Name: Allow Update Compliance Processing <BR>
* Description: Opts device data into Update Compliance processing. Required to see data. <BR>
* OMA-URI: ./Vendor/MSFT/Policy/Config/System/AllowUpdateComplianceProcessing <BR>
* Data type: Integer <BR>
* Value: 16 <BR>

![](https://github.com/mattnovitsch/M365/blob/main/UC14.jpg)

<BR>
21. Click Next to go to the Assignments tab. <BR>

![](https://github.com/mattnovitsch/M365/blob/main/UC15.jpg)
<BR>
22. I'm adding it to all my devices, I would recommend a pilot group if this is a production tenant. Click Next to go to applicability rules.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/UC16.jpg)
<BR>
23. I added a Rule that will make sure its my Windows 10 Enterprise devices that get this policy only. You can also apply it to certain versions of Windows. Click Next once you have added your rule.<BR>

![](https://github.com/mattnovitsch/M365/blob/main/UC17.jpg)
<BR>

Your Update compliance should now work, please note it takes up to 24 hours for data to start coming into the system. Mine was closer to 36, but I think it was because of all the changes I was making trying to force it. If you want you can also deploy the script found here: [Update Compliance Script](https://docs.microsoft.com/en-us/windows/deployment/update/update-compliance-configuration-script#how-to-use-this-script).