# Summary
I had a customer ask about configuring Teams to be deployed minimized. This can be done per user basis, but they were looking for doing it via global settings. PowerShell and Intune to the rescue! This article will walk you through deployment of the script I have found 

## Reference
* [AlkaneSolutions](https://www.alkanesolutions.co.uk/2021/01/16/launch-microsoft-teams-minimised-in-the-system-tray/)

## Prerequisites
* [EnableCheckspellingbeforesendingamessage.ps1](https://github.com/mattnovitsch/M365/blob/main/Checkspellingbeforesendingamessage/EnableCheckspellingbeforesendingamessage.ps1)

## Steps:
1. Navigate to [Microsoft Endpoint Manager](http://endpoint.microsoft.com)
2. Navigate to Reports > Endpoint Analytics
* Note: You can do this via scripts also but since we are trying to force this change in an organization having it run more than once is best handled in Endpoint Analytics<BR>
![image](https://user-images.githubusercontent.com/61195587/166960098-db8e95fa-3a83-47ce-b7b5-13a35afc4955.png)
3. Click on Proactive Remediations and then Create script package <BR>
![image](https://user-images.githubusercontent.com/61195587/166960369-4b4949d4-3f58-42dc-90c2-c6b635a8bd27.png)
4. Provide your script package a name. I'm naming mine "Deploying Teams Minimized" <BR>
![image](https://user-images.githubusercontent.com/61195587/166969960-122d1b96-5a20-4134-b0c5-68b21dee9511.png)
5. Upload the script that was download earlier as a prerequisite and make sure to change "Run this script using the logged-on credentials", this is important as the registry keys changed by the PowerShell are in HKeyCurrentUser. <BR>
![image](https://user-images.githubusercontent.com/61195587/166970211-cb03dd8a-352f-47e5-a6ce-582375e6ad1c.png)
6. Assign Tag accordingly <BR>
![image](https://user-images.githubusercontent.com/61195587/166970344-17c43a38-56cd-4064-9c7e-53e18c1c2470.png)
7. Assign to the correct group or all devices.
* Note: If you click Daily you can modify the run time from daily, hourly, or once. 
![image](https://user-images.githubusercontent.com/61195587/166970635-0510170a-d3c7-4087-8d13-f0169711046b.png)
8. Click Create after you review the configuration. <BR>
![image](https://user-images.githubusercontent.com/61195587/166970828-b7b24b68-651e-4771-85d2-884b04bd3607.png)

## Script deep dive
This script currently allows you to change three settings in the json: Open as hidden, Open at Login, and Running on close. The notes in the script are pretty detailed so I won't go into much details on them. OpenasHidden is the value you would want to be True for it to open minimized. The script does close teams then makes the change and reopens it. If all goes well the first run will close teams and appear to be done but if you open your system tray you will see it there. Follow up runs will not have any impact on the user. 

* Note: if you run this more than once it will still close Teams and reopen it, so depending on when the script fires off it could impact user experience

`#Open in the background`<BR>
`$openAsHidden=$true`<BR>
<BR>
`#Open after login`<BR>
`$openAtLogin=$true`<BR>
<BR>
`#Keep running in background when we 'close' teams`<BR>
`$runningOnClose=$true`<BR>
<BR>
`$jsonFile = [System.IO.Path]::Combine($env:APPDATA, 'Microsoft', 'Teams', 'desktop-config.json')`<BR>
      <BR>
`if (Test-Path -Path $jsonFile) {   `<BR>
   <BR>
    `#Get Teams Configuration`<BR>
    `$jsonContent =Get-Content -Path $jsonFile -Raw`<BR>
   <BR>
    `#Convert file content from JSON format to PowerShell object`<BR>
    `$jsonObject = ConvertFrom-Json -InputObject $jsonContent`<BR>
   <BR>
    `#Update Object settings`<BR>
        <BR>
        `if ([bool]($jsonObject.appPreferenceSettings -match "OpenAsHidden")) {`<BR>
            `$jsonObject.appPreferenceSettings.OpenAsHidden=$openAsHidden`<BR>
<BR>
        `} else {`<BR>
            `$jsonObject.appPreferenceSettings | Add-Member -Name OpenAsHidden -Value $openAsHidden -MemberType NoteProperty`<BR>
        `}`<BR>
    <BR>
        `if ([bool]($jsonObject.appPreferenceSettings -match "OpenAtLogin")) {`<BR>
            `$jsonObject.appPreferenceSettings.OpenAtLogin=$openAtLogin`<BR>
        `} else {`<BR>
            `$jsonObject.appPreferenceSettings | Add-Member -Name OpenAtLogin -Value $openAtLogin -MemberType NoteProperty`<BR>
        `}`<BR>
                <BR>
        `if ([bool]($jsonObject.appPreferenceSettings -match "RunningOnClose")) {`<BR>
            `$jsonObject.appPreferenceSettings.RunningOnClose=$runningOnClose`<BR>
        `} else {`<BR>
            `$jsonObject.appPreferenceSettings | Add-Member -Name RunningOnClose -Value $runningOnClose -MemberType NoteProperty`<BR>
        `}`<BR>
           <BR>
        `#Terminate Teams if it is running`<BR>
        `$teamsProcess = Get-Process Teams -ErrorAction SilentlyContinue`<BR>
	    `If ($teamsProcess) {`<BR>
<BR>
			    `#Close Teams Window`<BR>
  			    `$teamsProcess.CloseMainWindow() | Out-Null`<BR>
			    `Sleep 5`<BR>
		<BR>
           	    `#Close Teams `<BR>
			    `Stop-Process -Name "Teams" -Force -ErrorAction SilentlyContinue`<BR>
<BR>
	    `}`<BR>
<BR>
        `#Update configuration`<BR>
        `$jsonObject | ConvertTo-Json -Depth 5 | Set-Content -Path $jsonFile -Force`<BR>
         <BR>
        `#Define Teams Update.exe paths      `<BR>
        `$userTeams = [System.IO.Path]::Combine("$env:LOCALAPPDATA", "Microsoft", "Teams", "current", "Teams.exe")`<BR>
        `$machineTeamsX86 = [System.IO.Path]::Combine("$env:PROGRAMFILES (X86)", "Microsoft", "Teams", "current", "Teams.exe")`<BR>
        `$machineTeamsX64 = [System.IO.Path]::Combine("$env:PROGRAMFILES", "Microsoft", "Teams", "current", "Teams.exe")`<BR>
        <BR>
        `#Define arguments`<BR>
        `$args = @("-process-start-args","""--system-initiated""")`<BR>
<BR>
        `#Launch Teams`<BR>
        `if (Test-Path -Path $userTeams) {`<BR>
            `Start-Process -FilePath $userTeams -ArgumentList $args`<BR>
        `} elseif (Test-Path -Path $machineTeamsX86) {`<BR>
            `Start-Process -FilePath $machineTeamsX86 -ArgumentList $args`<BR>
        `} elseif (Test-Path -Path $machineTeamsX64) {`<BR>
            `Start-Process -FilePath $machineTeamsX64 -ArgumentList $args`<BR>
        `}`<BR>
<BR>
    `}`<BR>