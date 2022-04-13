# Summary
I was recently asked; can we move our remote users from local accounts to Azure AD accounts and keep their profiles? The answer is it depends on the applications that are the user is using. If the user is an office user that just uses Office products, then this can be done really easily. I'll walk you through the example of migrating a user that just uses Office and other minor applications that doesn't require customer configurations to move to an Azure AD account via OneDrive.

## Prerequisite
* OneDrive Licenses
* Intune Licenses and deployed to the machine

## Admin Steps
1. Navigate to [Microsoft Endpoint Manager](https://endpoint.microsoft.com/)
2. Navigate to Devices > Windows > Configuration Profiles, then click Create Profile <BR>
![image](https://user-images.githubusercontent.com/61195587/163179335-5a833bcc-69e6-4936-b51b-046178676a69.png)
3. Select the following then click Create:
* Platform: Windows 10 and later
* Profile Type: Templates
* Template Name: Administrative Templates <BR> 
![image](https://user-images.githubusercontent.com/61195587/163179782-2bddf66b-3f2c-4afe-89cf-052de4dfa2a0.png)
4. Name the profile something meaningful to your organization or project. I'm just calling it OneDrive for Business Profile. Click Next once you have named it.
![image](https://user-images.githubusercontent.com/61195587/163180139-38279508-93f0-4a4b-b3c5-56e0ce2492f0.png)
5. On the configuration settings section, scroll down to one drive. There are a lot of options here that your organization needs to define. Select what you need per your requirements. The ones I have selected pretty typical from what I have seen working with customers.<BR>
![image](https://user-images.githubusercontent.com/61195587/163181290-70826033-1981-4344-baf6-99f71031a9fe.png)
6. On the scope tags, make sure to assign this appropriately to the devices you have tagged(really important for RBAC). <BR>
![image](https://user-images.githubusercontent.com/61195587/163181661-b6afc0db-f1be-49a3-9430-59fd13445b13.png)
7. Select the group of devices you are applying this setting for, I would strongly recommend a test group first. The great thing about this setting is once its tested and validated that it works then you can apply it to all devices that use one drive. I have it deployed to all devices in my lab but everyone needs to evaluate what their organization needs are. <BR>
![image](https://user-images.githubusercontent.com/61195587/163182458-976d8d1d-f8c2-42f8-8aec-e96b29a6fe4e.png)
8. Review then click create to deploy your profile.

## User Steps
1. User will be prompted to sign into OneDrive with their Azure AD credentials. <BR>
![image](https://user-images.githubusercontent.com/61195587/163184429-82d25e1d-91c0-40d4-ba77-7e22337671b0.png)
2. Have them click next on the folder location <BR>
![image](https://user-images.githubusercontent.com/61195587/163184933-8d96106f-b20a-4b29-b414-bbab8994f2b9.png)
3. Enter the password to login <BR>
![image](https://user-images.githubusercontent.com/61195587/163187286-b34ef5c2-1686-4eda-aa6e-ae980423efe9.png)
4. Click Next informational window<BR>
![image](https://user-images.githubusercontent.com/61195587/163187365-1e805e24-8ef9-4b38-a10b-2135f5db6042.png)
5. Click next on the additional informational window <BR>
![image](https://user-images.githubusercontent.com/61195587/163187449-67314993-f44d-46ab-976d-5757af2741ab.png)
6. Click next on the final informational window <BR>
![image](https://user-images.githubusercontent.com/61195587/163187608-5989f148-70df-4e59-8bb0-8fac5f3980cc.png)
7. Click later on the mobile app screen <BR>
![image](https://user-images.githubusercontent.com/61195587/163187763-72d4810f-977d-4f9e-8023-c1ff2e227f06.png)
8. Close the window that confirms the setup <BR>
![image](https://user-images.githubusercontent.com/61195587/163187858-bd272d83-1cdf-4a8c-a844-e20606500b70.png)
9. The hardest part of this, waiting for all the their data to copy over to one drive. Since we are doing known folders only, it will only do whatever they have in Documents, Pictures, and Desktop. The timing on this will vary depending on how much the users have and how much bandwidth they have. Let's just say we waited a week to be safe. Everything is backed up now.
10. User logs in with their Azure AD credentials and onedrive begins to download the data from OneDrive to their Azure AD Profile on that workstation and you are complete.
