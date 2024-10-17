# Summary
We are going to walk through importing Entra ID groups. This article will assume you have already created the group in Entra.

## Steps
1. Navigate to [Defender XDR](https://security.microsoft.com/)
2. Navigate to Settings > Cloud Apps > System > User Groups
3. Click Import user group
![image](https://github.com/user-attachments/assets/0f7818d7-48d4-486d-be86-f8c7192bc068)

4. Select Office 365(Microsoft Entra ID) and type the name of your user group
5. Click Import

![image](https://github.com/user-attachments/assets/7401cb9c-88c0-486b-b89a-ca4b255062ff)

6. You have to wait for the import to complete before you can assign it to a group. You might see it in the list but until it has the desired number of members it won't apply.
** Note: This is important to remember when adding a user to the group, it won't take effect until Cloud Apps gets the update which could be an hour or so later from what I have seen.

![image](https://github.com/user-attachments/assets/f1ee1fd2-cb50-4e00-aa10-340049550c5b)
