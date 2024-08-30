# Summary
I've seen this asked before and there seems to be some confusion along how to get this data. I did some testing in my lab for this. There were a couple of "gotchas" in the mix, but it is possible. 

If the account is local, we wouldn't have a SID in Entra ID or On-prem AD to compare to.
If the account was on-prem or Entra ID, the information for what the customer is looking for won't be available without MDI deployed.
The identity information in the IdentityInfo table for the account doesn't match up to the SID column in the DeviceEvents table.

DeviceEvents SID =AccountSid <BR>
IdentityInfo SID = CloudSID or OnPremSid

I came up with three different queries:
* Find newly created local account added to group
* Find cloud or on-prem accounts added to group
* Find local account that was recently logged in with that had a group membership change

![image](https://github.com/user-attachments/assets/ad64dafc-d975-485c-8524-244933220a7b)

## KQL Download
KQL can be found [here](https://github.com/mattnovitsch/M365/blob/main/KQL/MDE/MDE-FindAccountsAddedtoGroup).