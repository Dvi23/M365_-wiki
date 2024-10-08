# Summary

The purpose of this document is to provide guidance on deployment rings for Defender for Endpoint. This document will cover Intune, GPO, Configuration Manage/WSUS. Additional information covered will include Linux and MacOS.

## Ring Information

This won't be like most of my documents as it will depend greatly on each environment. Please note that not all the channels are available for each Defender Update Feature:

![image](https://github.com/user-attachments/assets/fdb14407-5ed5-49d9-bd28-4e684ec23c0d)

### Beta
This is for insider preview so I would imagine most customers won't be using this. If you have engineers that would be testing new features this is where we would put them.

### Current Channel (Preview)
First let's discuss the different ring options. Most customers will use Current Channel (Preview) for your pre-production environments and/or IT department devices. 

### Current Channel (Staged)
Current Channel (Staged) is recommended for users on the floor that would provide valuable feedback. A person per department would be helpful and recommended.

* Valuable feedback: System is running slow after updates; my RAM is at XX% and is not going down. I can see the Defender service is running high.
* Nonvaluable feedback: My system is slow, please fix.

### Current Channel (Broad)
This is going to be the majority of your environment.

### Critical
These would be systems or users that you see as critical to your environment. Examples of these would be health care systems, banking systems, and anything else you might classify as critical in your environment.

<BR>

![image](https://github.com/user-attachments/assets/e9c741d5-b17d-4759-bc7f-8ca4b4041e10)

## Windows Deployment
Once you figured out what channels you are going to use then we have to deploy them.

***

* Intune - I would strongly encourage using the Defender Update Controls under Endpoint Security > Antivirus. This will allow you to create Entra Groups that you can place user/devices in the groups for each defined ring. 

![image](https://github.com/user-attachments/assets/af30da04-aee4-4737-ae0e-b0e450347377)


***

* Group Policy Object (GPO) - You will need to download the latest Windows Defender .admx and .adml and install them on your Domain Controller.

1. [WindowsDefender.admx](https://github.com/microsoft/defender-updatecontrols/blob/main/WindowsDefender.admx)
2. [WindowsDefender.adml](https://github.com/microsoft/defender-updatecontrols/blob/main/WindowsDefender.adml)

You will need to open the Group Policy Object and navigate to Computer Configuration > Administrative Templates > Windows Components > Microsoft Defender Antivirus. There are three settings you need to configure.

1. Select the channel for Microsoft Defender daily security intelligence updates
2. Select the channel for Microsoft Defender monthly engine updates
3. Select the channel for Microsoft Defender monthly platform updates

![image](https://github.com/user-attachments/assets/9873728c-452c-437e-8b7c-3ed0d1ea73ce)

You will need to do this for each ring you plan to deploy.

***

* Configuration Manager/WSUS - If you are already using these applications or similar ones, then you are already set in the ring deployment method most likely. If you follow the guidance above, then you will get the updates rolled out in a staged deployment. The only other guidance I would recommend is checking to make sure that your Software Update Point/WSUS has the following enabled to download the updates.

![image](https://github.com/user-attachments/assets/f5134df3-c628-4b6d-ba1a-275f6ab9b9ea)

## Linux Deployment

This one is probably the easiest. Microsoft has a [Repository](https://packages.microsoft.com/) for all its updates and versions of Linux we support. When you point to the repository, you can select the folder you want to download and configure per Linux Device. You can configure cron jobs and set timers accordingly per linux device. For information on setting up the cron jobs please see - [Schedule an update of the Microsoft Defender for Endpoint (Linux)](https://learn.microsoft.com/en-us/defender-endpoint/linux-update-mde-linux#for-those-who-use-ansible-chef-or-puppet)

![image](https://github.com/user-attachments/assets/825ace94-3ed6-4dc8-940d-3afe3b4c50f2)

This is probably the closest I could come to ring mapping for Linux:
* Insider_fast = Channel (UAT)
* Insider_slow = Channel (DEV)
* Prod = Current Channel (Broad)

## MacOS Deployment

For MacOS we need to configure the plist for each group. This can be done via Intune, JAMF, or whatever tool you are using to push the configuration.
The plist must include ChannelName with a string value of one of the following:

* Beta Channel
* Current Channel (Preview)
* Current Channel

Microsoft has documented examples of the plist file [here.](https://learn.microsoft.com/en-us/defender-endpoint/mac-updates#jamf-pro)

## Validation

Now we need to validate all the endpoints are working as configured and in the correct rings. We could go to each device, but it's much quicker to do it from Advance Hunting query. As you can see from the image below the query captures Active devices, last time they were updated, what version everything is, and their assigned rings. You can get a copy of the KQL from [here.](https://github.com/mattnovitsch/M365/blob/main/KQL/MDE/DeviceInventory.txt)

![image](https://github.com/user-attachments/assets/d9020a6e-fa23-46ce-8304-a190fc0873c8)


## References
Microsoft Latest Antimalware Changes: [Antimalware updates change log - Microsoft Security Intelligence](https://www.microsoft.com/en-us/wdsi/definitions/antimalware-definition-release-notes)

Microsoft Latest updates: [Latest security intelligence updates for Microsoft Defender Antivirus and other Microsoft antimalware - Microsoft Security Intelligence](https://www.microsoft.com/en-us/wdsi/defenderupdates)

Rings:
* [Microsoft Defender Antivirus ring deployment guide overview - Microsoft Defender for Endpoint | Microsoft Learn](https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-antivirus-ring-deployment)
* [Manage the gradual rollout process for Microsoft Defender updates - Microsoft Defender for Endpoint | Microsoft Learn](https://learn.microsoft.com/en-us/defender-endpoint/manage-gradual-rollout#update-channels-for-monthly-updates)

CSP Ring Value: [Defender CSP | Microsoft Learn](https://learn.microsoft.com/en-us/windows/client-management/mdm/defender-csp#configurationplatformupdateschannel)

Safe Deployment Practices: 
[Microsoft Defender for Endpoint’s Safe Deployment Practices](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/microsoft-defender-for-endpoint-s-safe-deployment-practices/ba-p/4220342)

Linux Respository: https://packages.microsoft.com/

MacOS: [Deploy updates for Microsoft Defender for Endpoint on Mac - Microsoft Defender for Endpoint | Microsoft Learn](https://learn.microsoft.com/en-us/defender-endpoint/mac-updates#set-preferences-for-microsoft-autoupdate)
