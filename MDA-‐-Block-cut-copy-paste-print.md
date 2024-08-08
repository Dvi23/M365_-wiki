# Summary
Blocking cut, copy, paste, and printing is something we might want to do for devices that are BYOD. A common situation is allowing users to check their emails at home but making sure they don't copy data off to their personal devices.

## Prerequisites
* [Conditional Access Application Control](https://github.com/mattnovitsch/M365/wiki/MDA-%E2%80%90-Conditional-Access-Application-Control)

## Steps to prevent cut/copy/paste/print
1. Navigate to [Defender XDR](https://security.microsoft.com)
2. Navigate to Cloud Apps > Policies > Policy Management > Create Policy > Session Policy
![image](https://github.com/user-attachments/assets/39182e34-b514-4d53-b21b-e3c0d3cf4c09)

3. Give your policy a name for example "Block cut/copy/paste/print"
4. Under Session Control Type: Select Block Activities
5. Under "Activities matching all of the following"
 a. Device is optional (However the default is for a BYOD situation)
 b. App is for any application you want, if you want all of them then just remove it.
 c. Activity Type should equal what function you want to block. I selected all for this example.
6. If you want to use the labels from Purview you can do that to prevent just those items from being cut, copy, paste, and printed.
7. Under Actions, we want to block.
* Note you can add a custom block message to your environment
8. I would strongly recommend turning off Alerts for this policy so you are not spammed with alerts that you would just have to close. You can do reporting data in Advance Hunting if you want to see the data.
9. Save Policy
* Note the policy will take effect next time you close the sessions and re-establish a connection. It will NOT apply to current sessions.
* Also Note the screenshot below is for blocking print, paste, copy and cut for all cloud apps for Soren when he is not on a corporate managed device.
![image](https://github.com/user-attachments/assets/f17a5e97-f1ce-479a-a462-6c513242e038)
