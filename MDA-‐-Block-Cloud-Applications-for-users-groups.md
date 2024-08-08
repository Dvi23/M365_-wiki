# Summary
Blocking cloud applications for users and/or groups. This is something organizations want to allow say Dropbox or Netflix for a set of users.

## Prerequisites
* [Conditional Access Application Control](https://github.com/mattnovitsch/M365/wiki/MDA-%E2%80%90-Conditional-Access-Application-Control)

## Steps to block cloud applications
1. Navigate to [Defender XDR](https://security.microsoft.com)
2. Navigate to Cloud Apps > Policies > Policy Management > Create Policy > Access Policy
![image](https://github.com/user-attachments/assets/6f8dab29-f422-4c5c-936c-ccc4a845cd3e)
3. Give your policy a name for example "Block Access to app for users/groups"
4. Delete Device under "Activities matching all of the following" and add User > Name or From Group > equals > "The user or group you want to block"
5. Under Actions select Block.
* Note: You can add a custom message if you like.
6. I would strongly recommend turning off Alerts for this policy so you are not spammed with alerts that you would just have to close. You can do reporting data in Advance Hunting if you want to see the data.
![image](https://github.com/user-attachments/assets/07abe557-89f8-4d00-b870-9803d59bc1e4)
7. Save Policy

* Note the policy will take effect next time you close the sessions and re-establish a connection. It will NOT apply to current sessions.

