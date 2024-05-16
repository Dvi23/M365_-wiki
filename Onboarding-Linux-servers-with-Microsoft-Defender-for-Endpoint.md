## Summary:
This will walk you through the process of onboarding Microsoft Defender for Endpoint on Redhat Linux devices.

## Deployment Steps:
1.	Now we need to download the onboarding script to your workstation from Defender XDR: <BR>
Navigate to https://security.microsoft.com/ 

2.	Navigate to Settings > Endpoints > Onboarding
3.	Select Linux Servers and then Download onboarding package.
![image](https://github.com/mattnovitsch/M365/assets/61195587/acf91c0a-5062-4162-b44e-c7e59550eeb0)

4.	Unzip the file and remember its location.
![image](https://github.com/mattnovitsch/M365/assets/61195587/e680826d-9bd5-4a03-a292-ece2abc3b61c)

5.	Open an Administrative PowerShell.
6.	We will use the SCP command to upload the py script to the Linux Server: <BR>
`scp -P 22 .\MicrosoftDefenderATPOnboardingLinuxServer.py <username>@<IP Address or servername>:/home/<username>/Desktop/`<BR>
•	It should prompt you for your password. <BR>
![image](https://github.com/mattnovitsch/M365/assets/61195587/6411db44-339e-460a-896d-c39c9c627e1b)

7.	Check and/or Install Python. <BR>
`python --version`<BR>
`sudo dnf install python3`
7.	Install MDE<BR>
`sudo yum install mdatp`
8.	Change directory to the location where you placed the onboarding package.<BR>
`cd Desktop`
9.	Run the python script to create the onboarding package.<BR>
`sudo python MicrosoftDefenderATPOnboardingLinuxServer.py`
10.	Check the MDE client is pointing to your tenant: <BR>
`mdatp health --field org_id`
 
11.	You should see your OrgID returned, if you do then you are complete. It should show up in the console within 15 minutes to a couple of hours(mine were both in 15 minutes).

## Troubleshooting Steps:
If you need to turn off or uninstall MDE from the device:
* For Uninstall: `sudo yum remove mdatp`
* For stopping the service: `sudo service mdatp stop`
* For restarting the service:`sudo service mdatp restart`

## Official references and sources:
* [Deploy Microsoft Defender for Endpoint on Linux manually](https://learn.microsoft.com/en-us/defender-endpoint/linux-install-manually#rhel-and-variants-centos-fedora-oracle-linux-amazon-linux-2-rocky-and-alma)<BR>
* [Troubleshoot installation issues for Microsoft Defender for Endpoint on Linux](https://learn.microsoft.com/en-us/defender-endpoint/linux-support-install)
* [Microsoft Defender for Endpoint on Linux - Support Versions of Linux](https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-endpoint-linux#system-requirements)

## Next Steps:
Now that we have the Linux device onboarded with MDE, we need to push policies to them. Please see the next section: [How to push policy to Linux devices from Intune](https://github.com/mattnovitsch/M365/wiki/How-to-push-policy-to-Linux-devices-from-Intune)