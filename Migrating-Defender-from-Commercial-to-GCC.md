Migrating from Microsoft Defender for endpoint client from Commercial to GCC tenant. This is assuming you have already worked with your CSAM and the Microsoft Transition team and have already onboarded one device to the new GCC tenant first. This is required as backend tenant information needs to be configured. 


Option 1: Using Intune to Migrate agents into GCC Tenant.
1.	Navigate to Intune Admin Center (https://intune.microsoft.com/ )
2.	Select Endpoint Security on the left hand side
3.	Select Endpoint Detection and Response
4.	Select Create New Policy
5.	For Platform select Windows 10, Windows 11, and Windows Server and for Profile select Endpoint Detection and Response
6.	Select the Create button
 
![image](https://github.com/mattnovitsch/M365/assets/61195587/bc618214-dee9-4210-be9d-25cedfb8473a)

7.	Give a name to your policy <BR>
![image](https://github.com/mattnovitsch/M365/assets/61195587/90f1c294-e625-4a53-96fb-3a056a6bbaf1)
 
8.	Select one of the following options: Auto from connector or Onboard. If you select Auto from connector you have to make sure the connector between Intune and Defender for endpoint is established. For onboard you will need to download the script from the Defender XDR portal. This example will be for onboard.
![image](https://github.com/mattnovitsch/M365/assets/61195587/47dc8724-e3e0-453b-aa35-d8ed5170bcbc)
  
9.	Navigate to Defender XDR in another browser tab(https://security.microsoft.com/ )
10.	Click on Settings
11.	Scroll down and select Onboarding
12.	Change Deployment Method to Mobile Device Management/ Microsoft Intune
13.	Select Download onboarding package
![image](https://github.com/mattnovitsch/M365/assets/61195587/360c4d24-79db-416d-acb7-08e922d31573)
 
14.	Open File once it has completed downloading <BR>
![image](https://github.com/mattnovitsch/M365/assets/61195587/691f7808-de4d-4da9-afb4-83ce897a530f)
 
15.	Open WindowsDefenderATP.onboarding with notepad or some other text editor program.
![image](https://github.com/mattnovitsch/M365/assets/61195587/9bab3b9a-bb3a-4855-9580-108937519ba2)
  
16.	Copy the entire contents of the file (ctrl+a then ctrl+c) <BR>
![image](https://github.com/mattnovitsch/M365/assets/61195587/8e021c9b-b2de-49c5-9541-3e6498e97110)
  
17.	Navigate back to Intune Admin Center tab.
18.	Paste the script into the Onboarding section
19.	Set Sample Sharing to All(Default)
20.	Set Telemetry Reporting Frequency to Normal
![image](https://github.com/mattnovitsch/M365/assets/61195587/b694c361-c22f-4305-87a6-dd1d2e9bdb45)
  
21.	Add any scope tags and select Next
![image](https://github.com/mattnovitsch/M365/assets/61195587/ca3d99cf-20c5-43ed-8498-f33f4bcd7f8d)
  
22.	Put in a test group that you want to onboard first. Small percentage 5-10 would be good.
23.	Select Next <BR>
![image](https://github.com/mattnovitsch/M365/assets/61195587/9fc66b5b-9b9d-4392-aecc-454ba99a06ac)
 
24.	Review the settings then click Save
![image](https://github.com/mattnovitsch/M365/assets/61195587/c22a6706-4fc5-487c-b324-d6e0d9604435)
 
Note: A reboot is required for these changes to take effect. Once the system is rebooted, it should appear in the GCC tenant within 1-2 hours. If you run into problems, please reach out to your CSAM or FTA/FM for assistance. If you don't have a CSAM or FTA/FM you can put in a request for assistance at [Fast Track](http://www.microsoft.com/fasttrack). Fast Track can walk you through the process.