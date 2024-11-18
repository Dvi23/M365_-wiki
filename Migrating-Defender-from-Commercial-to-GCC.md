Migrating from Microsoft Defender for endpoint client from Commercial to GCC tenant. This is assuming you have already worked with your CSAM and the Microsoft Transition team and have already onboarded one device to the new GCC tenant first. This is required as backend tenant information needs to be configured. Quick link to this page: [https://aka.ms/DefenderCommercialtoGCCDoc](https://aka.ms/DefenderCommercialtoGCCDoc)

1. Have CSAM open transition ticket to make. 
2. Once the transition is complete and the single device is in the GCC Defender XDR Portal, migrate the Intune/ConfigManager/GPO: 
Using Intune to Migrate agents into GCC Tenant.
* Navigate to Intune Admin Center (https://intune.microsoft.com/ )
* Select Endpoint Security on the left hand side
* Select Endpoint Detection and Response
* Select Create New Policy
* For Platform select Windows 10, Windows 11, and Windows Server and for Profile select Endpoint Detection and Response
* Select the Create button
 
![image](https://github.com/mattnovitsch/M365/assets/61195587/bc618214-dee9-4210-be9d-25cedfb8473a)

* Give a name to your policy <BR>
![image](https://github.com/mattnovitsch/M365/assets/61195587/90f1c294-e625-4a53-96fb-3a056a6bbaf1)
 
* Select one of the following options: Auto from connector or Onboard. If you select Auto from connector you have to make sure the connector between Intune and Defender for endpoint is established. For onboard you will need to download the script from the Defender XDR portal. This example will be for onboard.
![image](https://github.com/mattnovitsch/M365/assets/61195587/47dc8724-e3e0-453b-aa35-d8ed5170bcbc)
  
* Navigate to Defender XDR in another browser tab(https://security.microsoft.com/ )
* Click on Settings
* Scroll down and select Onboarding
* Change Deployment Method to Mobile Device Management/ Microsoft Intune
* Select Download onboarding package
![image](https://github.com/mattnovitsch/M365/assets/61195587/360c4d24-79db-416d-acb7-08e922d31573)
 
* Open File once it has completed downloading <BR>
![image](https://github.com/mattnovitsch/M365/assets/61195587/691f7808-de4d-4da9-afb4-83ce897a530f)
 
* Open WindowsDefenderATP.onboarding with notepad or some other text editor program.
![image](https://github.com/mattnovitsch/M365/assets/61195587/9bab3b9a-bb3a-4855-9580-108937519ba2)
  
* Copy the entire contents of the file (ctrl+a then ctrl+c) <BR>
![image](https://github.com/mattnovitsch/M365/assets/61195587/8e021c9b-b2de-49c5-9541-3e6498e97110)
  
* Navigate back to Intune Admin Center tab.
* Paste the script into the Onboarding section
* Set Sample Sharing to All(Default)
* Set Telemetry Reporting Frequency to Normal
![image](https://github.com/mattnovitsch/M365/assets/61195587/b694c361-c22f-4305-87a6-dd1d2e9bdb45)
  
* Add any scope tags and select Next
![image](https://github.com/mattnovitsch/M365/assets/61195587/ca3d99cf-20c5-43ed-8498-f33f4bcd7f8d)
  
* Put in a test group that you want to onboard first. Small percentage 5-10 would be good.
* Select Next <BR>
![image](https://github.com/mattnovitsch/M365/assets/61195587/9fc66b5b-9b9d-4392-aecc-454ba99a06ac)
 
* Review the settings then click Save
![image](https://github.com/mattnovitsch/M365/assets/61195587/c22a6706-4fc5-487c-b324-d6e0d9604435)

3. If you are using Defender for Cloud and ARC([Migrate to tenant from Public to GCC (Gov) - Overview](https://dev.azure.com/ASIM-Security/Infrastructure%20Solutions/_wiki/wikis/Defender%20for%20Cloud/2518/Migrate-to-tenant-from-Public-to-GCC-(Gov))): 
* Turn off the 'Endpoint protection' MDC component:
* MDC Environment settings
* Select the subscription
* In the Defenders plans page, select the Settings & monitoring button at the top
* Turn Off the Endpoint protection component
* Select 'Continue'
* Select 'Save'
* Delete the VM Extension from the machines
* Follow [Offboard devices](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/offboard-machines?view=o365-worldwide)  to offboard all servers.
* Have customer execute [https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell scripts/MDE Integration/Migrate GCC Tenant](https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/MDE%20Integration/Migrate%20GCC%20Tenant) 
* Turn the 'Endpoint protection' MDC component back on.
* VM's will be provisioned with VM Extension and will be onboarded to GCC

4. If you are using Sentinel, you will need to setup a GCC workspace for Sentinel, then you will be able to send data from Defender XDR in GCC to Sentinel.

5. Once customer has confirmed all endpoints are moved out of commercial, put in a ticket for the Defender Commercial tenant to be deleted.


 
Note: A reboot is required for these changes to take effect. Once the system is rebooted, it should appear in the GCC tenant within 1-2 hours. If you run into problems, please reach out to your CSAM or FTA/FM for assistance. If you don't have a CSAM or FTA/FM you can put in a request for assistance at [Fast Track](http://www.microsoft.com/fasttrack). Fast Track can walk you through the process.