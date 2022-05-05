# Summary
I had a customer ask about configuring Outlook for all their users to always spell check their emails before sending a message. I have written a script that will do this.

* Note: The script is written for Office 365 current branch if you are using an older version of Office then you will need to change the script version number from 16.0 to whatever version you are using.

![image](https://user-images.githubusercontent.com/61195587/166957927-308c1f95-b87a-4f8e-b0f1-83457e558119.png)

## Prerequisites
* [EnableCheckspellingbeforesendingamessage.ps1](https://github.com/mattnovitsch/M365/blob/main/Checkspellingbeforesendingamessage/EnableCheckspellingbeforesendingamessage.ps1)

## Steps:
1. Navigate to [Microsoft Endpoint Manager](http://endpoint.microsoft.com)
2. Navigate to Reports > Endpoint Analytics
* Note: You can do this via scripts also but since we are trying to force this change in an organization having it run more than once is best handled in Endpoint Analytics
![image](https://user-images.githubusercontent.com/61195587/166960098-db8e95fa-3a83-47ce-b7b5-13a35afc4955.png)
3. Click on Proactive Remediations and then Create script package <BR>
![image](https://user-images.githubusercontent.com/61195587/166960369-4b4949d4-3f58-42dc-90c2-c6b635a8bd27.png)
4. Provide the package with a name. I'm using "Check spelling before sending a message in Outlook". Click Next once you have established a name. <BR>
![image](https://user-images.githubusercontent.com/61195587/166960530-81b0df86-0c61-4375-a7a2-9117f0a08f0d.png)
5. Upload the script that was download earlier as a prerequisite and make sure to change "Run this script using the logged-on credentials", this is important as the registry keys changed by the PowerShell are in HKeyCurrentUser. <BR?
![image](https://user-images.githubusercontent.com/61195587/166961579-2bfdd096-71fa-4edf-a7f4-1144ba3640bf.png)
6. Assign Tag accordingly <BR>
![image](https://user-images.githubusercontent.com/61195587/166966275-b66aa967-f9d2-44bd-aa53-cb622f880876.png)
7. Assign to the correct group or all devices.
* Note: If you click Daily you can modify the run time from daily, hourly, or once. 
![image](https://user-images.githubusercontent.com/61195587/166966457-713f1074-0735-4984-b8b5-7240dabfaf4d.png)
8. Click Create after you review the configuration. <BR>
![image](https://user-images.githubusercontent.com/61195587/166966812-7a44c0f6-83ed-4a97-b83e-e01e97b9e408.png)

## Script deep dive
The $registryPath is the part I mentioned before about the different office versions. As you can see I am using the value of 16.0 so that is clearly 2016 or later. The script will check if the value of spell checker is enabled, if its not enabled the script will change it. If the script determines its also set to enabled then it just terminates. <BR> 
`#Define variables for the path, key, and value` <BR>
`$registryPath = "HKCU:\Software\Microsoft\Office\16.0\Outlook\Options\Spelling"`<BR>
`$Name = "check"`<BR>
`$value = "1"`<BR>
<BR>
`#check the path and key to see if its enabled or not.`<BR>
`#0 = disabled`<BR>
`#1 = enabled`<BR>
`If((Get-ItemProperty -Path HKCU:\Software\Microsoft\Office\16.0\Outlook\Options\Spelling\).check -eq 0)`<BR>
`{`<BR>
    `New-ItemProperty -Path $registryPath -Name $name -Value $value -PropertyType DWORD -Force | Out-Null`<BR>
`}`<BR>

