# Summary
I have some customer asking about blocking specific applications using AppLocker and how to manage it. I have done some digging and found that the software engineer that is responsible for the code created a really nice wizard to make it easier to deploy. The other call out here is that Applocker evolved to Windows Defender for Applicaiton Control and again to Application Control for Business.

## Prerequisites
* [App Control Policy Wizard](https://webapp-wdac-wizard.azurewebsites.net/)

## Setup
Get a list of files, folder locations, or drivers you want to block from running in the environment.
* Example: Notepad.exe, Java version from running, or blocking executables from running in a certain folder.

Assuming you have list of at least a couple or one item you want blocked we can move to opening the App Control Policy Wizard.
![image](https://github.com/user-attachments/assets/df1a6817-6d18-475c-899c-5409ffd47cac)

For this example, we are going to assuming you are creating this from scratch. We are going to create a Base Policy with Multiple Policy Format support.
![image](https://github.com/user-attachments/assets/05371f80-68a7-4a81-b171-fa2ca9cdd1be)

The base template is created of your current requirements and what you plan on locking down. I'm going to assume you want to start off with either All Microsoft Mode or Signed and Reputable Mode. This would depend a lot on what your current list that you have found in your environment. Either way we can do this in Audit mode so it's not going to hurt anything in your environment and limit the deployment to a test device or two. Let's select Signed and Reputable Mode. Provide the Policy with a name. WDAC default policy might be a good start.

![image](https://github.com/user-attachments/assets/9981ddb0-569d-42ba-9b66-16390975a608)

Policy Rules are pre-set based on the templates you have chosen. You can hover of each and they will tell you a short description of what they do. There is also a reference for a detailed list here: [Understand App Control for Business policy rules and file rules](https://learn.microsoft.com/en-us/windows/security/application-security/application-control/app-control-for-business/design/select-types-of-rules-to-create). From the screenshot below, you can see I am turning off Audit Mode, but I would highly encourage you keeping it in audit mode you plan on deploying this enterprise wide. If you are deploying to a single device then turning off Audit Mode would be recommended as we need to test it.

![image](https://github.com/user-attachments/assets/a9038d86-c862-49fd-9867-78151d4932bb)

Files Rules is where we can create allow or deny rules for files based on published, path, file attributes or hash values. I had a customer ask about blocking Java JRE version from running. We can do that multiple ways, either block the installation or block the exe from running. The option will depend on what your current situation is. In most cases, I would imagine that Java would already be installed so we would need to block both the installation location and install file.

![image](https://github.com/user-attachments/assets/7eee6371-f17b-44fa-b54a-9e24202bea17)


Clicking the +Add Custom link in the top right will allow you add these rules. Let's change the Rule Action to Deny and the Rule Type to File Attributes. Browse for the file you want to block. In this case, I am blocking Java JRE version 8.431. You will see if fills in the file attributes for the file. Check off all the boxes that apply. This will block the file from being able to run and prevent the installation of it.

![image](https://github.com/user-attachments/assets/a77f6802-9712-4c84-8869-e36c899ef5b5)

Let's block a folder that could have executables next. In this example, I have a folder on the root of my C drive called Block. Click +Add Custom again and change the Rule Action to Deny and the Rule Type to Path. Browse to the location and select the folder.

![image](https://github.com/user-attachments/assets/224edc3d-cd2e-4048-b8a0-e1a32d208f4a)

Keep adding all the rules for files or folder you want to block.

![image](https://github.com/user-attachments/assets/3b8fe940-3d97-4fbb-8ff3-cc9efa6f9054)

The policy should create in a minute or so and give you the output location.

![image](https://github.com/user-attachments/assets/c6c0549a-6255-4af7-bb82-b84b89826f48)

To test this on your device, copy the .cip file and copy it to C:\Windows\System32\CodeIntegrity\CiPolicies\Active on your test device, restart the device for the changes to take effect.

![image](https://github.com/user-attachments/assets/b4986c3e-ac56-4f09-9302-794cdc928981)

Now we need to test this out. Place an executable in C:\Block and try to open it. You should get the following.

![image](https://github.com/user-attachments/assets/a366b4ba-198f-4cff-84ba-0b226289ab7c)

You should see something very similar when you try to run the Java JRE version.

![image](https://github.com/user-attachments/assets/628d8505-8fc9-4b14-a331-8813418e6c9f)

Things to watch out for, if you want to block Notepad.exe for example, then you need to make sure you grab the correct one. There are currently two version on systems if they are pulling the latest from Windows Store. 

New location: C:\Program Files\WindowsApps\Microsoft.WindowsNotepad_11.2409.9.0_x64__8wekyb3d8bbwe\Notepad\

Old location: C:\Windows\Notepad.exe

With the rule I have below it will block the old location but not the new location.

![image](https://github.com/user-attachments/assets/39981710-2ba2-4cce-b317-245bcb7fafe9)

When you are ready to push to more than one device you can send the policy out via Intune. Navigate to Endpoint Security > App Control for Business. Create a new policy, when you get to the configuration settings import the xml file you created.

![image](https://github.com/user-attachments/assets/ff6ba2df-1a54-45ee-8d21-56bcd4dac0d8)

Deploy the policy to your target group.

Good luck with your Application Control Policy and testing.


## References:
* [Understand App Control for Business policy rules and file rules](https://learn.microsoft.com/en-us/windows/security/application-security/application-control/app-control-for-business/design/select-types-of-rules-to-create)
* [App Control Policy Wizard](https://webapp-wdac-wizard.azurewebsites.net/)
* [Deploying App Control for Business policies](https://learn.microsoft.com/en-us/windows/security/application-security/application-control/app-control-for-business/deployment/appcontrol-deployment-guide)
