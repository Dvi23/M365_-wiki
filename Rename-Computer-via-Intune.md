# Summary
This script can be used to rename your computer with adding the device serial number in the name. I have had this request come up with several customers looking to do this during the enrollment process in Intune and/or AutoPilot. As the Intune does support serial number, autopilot doesn't support variables such as %SERIAL% and only support prefixes for the computer name. The plan would be to get the device to join with a temporary name then have it rename once it has fully enrolled with Intune. The renamecomputer.ps1 script will rename the device to Lenovo<serialnumber>. Please feel free to edit the script to whatever 6-character prefix you want. I also added a restart-computer command in there that is commented out, if you want to force the restart right after the change you can but I would just let it wait until the user does it on their own.

## Note
Active Directory limits to 15-characters so please make sure your prefix and serial number don't exceed that or it will fail. It's worth to note that if you don't have access to the domain controller for hybrid join this could cause domain trust issues with those devices.

## References
[Accounts Configuration Service Provider](https://docs.microsoft.com/en-us/windows/client-management/mdm/accounts-csp)<BR>
[Deploy hybrid Azure AD-joined devices by using Intune and Windows Autopilot](https://docs.microsoft.com/en-us/mem/autopilot/windows-autopilot-hybrid)

## Prerequisite
[RenameComputer.ps1](https://github.com/mattnovitsch/M365/blob/main/RenameComputer/RenameComputer.ps1)

## Steps
1. Navigate to [Microsoft Endpoint Manager](https://endpoint.microsoft.com/)
2. Navigate to Devices > Windows > PowerShell Scripts then click the +Add button <br>
![RenameComputer1](https://user-images.githubusercontent.com/61195587/162959130-8f7bc63b-f91b-43d6-aa65-cb93876cd2fd.jpg)
3. Name your script, I'm using "Rename Computer" for this example, click next to continue
![RenameComputer2](https://user-images.githubusercontent.com/61195587/162959943-229cd6e9-c77b-404e-80e8-4b8f21297131.jpg)
4. Select the RenameComputer.ps1 file then select next <br> 
![RenameComputer3](https://user-images.githubusercontent.com/61195587/162960065-7a706844-5d5f-4247-9507-3bacdcbadab1.jpg)
5. Scope the script appropriately, in my lab I only have one scope for windows devices. Click Next to continue <br>
![RenameComputer4](https://user-images.githubusercontent.com/61195587/162960517-784793e4-17ef-44c7-bc01-7633f184df3a.jpg)
6. The assignment is where it gets tricky. We only want to target the devices you want to rename. You can use your autopilot group but if you have devices already deployed it could rename devices that you don't want to. For safety reasons, I recommend creating a group that you want to target to rename and add it to the assignment. Click Next once you have selected your group <br>
![RenameComputer5](https://user-images.githubusercontent.com/61195587/162961534-e7f57a6a-0cc2-485c-a8d3-5396dede1167.jpg)
7. Review to make sure you have the correct script and group assigned. Click Add once you have verified everything <br>
![RenameComputer6](https://user-images.githubusercontent.com/61195587/162961730-10896e12-6147-4ac9-aa8f-86f4ab23a1fe.jpg)

