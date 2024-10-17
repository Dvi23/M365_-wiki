# Summary
Blocking cloud applications for users and/or groups. This is something organizations want to allow say Dropbox or Netflix for a set of users.

## Prerequisites
* [Conditional Access Application Control](https://github.com/mattnovitsch/M365/wiki/MDA-%E2%80%90-Conditional-Access-Application-Control)

## Steps to block cloud applications
1. Navigate to [Defender XDR](https://security.microsoft.com)
2. Navigate to Cloud Apps > Policies > Policy Management > Create Policy > Access Policy
![g04d4mng](https://github.com/user-attachments/assets/3c20e9d0-e75e-4f67-9d29-e7bd7007d4ec)
3. Give your policy a name for example "Block Access to app for users/groups"
4. Delete Device under "Activities matching all of the following" and add User > Name or From Group > equals > "The user or group you want to block" <BR>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Note: Alternatively: You can block this for everyone except for a Group of users. This would be like blocking Netflix for everyone except for Netflix_Allow_Group.
5. Under Actions select Block.
* Note: You can add a custom message if you like.
6. I would strongly recommend turning off Alerts for this policy so you are not spammed with alerts that you would just have to close. You can do reporting data in Advance Hunting if you want to see the data.
![08y6cfzi](https://github.com/user-attachments/assets/5022789e-10ee-4680-adc6-5236cb5da54c)

7. Save Policy

* Note the policy will take effect next time you close the sessions and re-establish a connection. It will NOT apply to current sessions.

