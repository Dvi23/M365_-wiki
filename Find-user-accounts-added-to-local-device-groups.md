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

DeviceEvents
| extend placeholder=1
| where ActionType contains "UserAccountAddedToLocalGroup"
| extend Fields=parse_json(AdditionalFields)
| extend AddToGroup = tostring(Fields.GroupName)
| extend GroupDomainName = tostring(Fields.GroupDomainName)
| join kind=inner (IdentityInfo 
    | extend placeholder=1
    | distinct AccountName, OnPremSid, CloudSid, placeholder
) on placeholder
| where AccountSid == OnPremSid or AccountSid == CloudSid
| project Timestamp, DeviceName, ActionType, AccountAdded=AccountName1, AddToGroup, GroupDomainName, AdditionalFields


//Find local account that was recently logged in with that had a group memebership change.

The first one will find if a local account is created then added to a group. You can see from the screenshot that I was able to get the accounts that were recently created and added to groups.
![image](https://github.com/user-attachments/assets/ee253716-8d29-43a2-bf43-afbd4b9d233f)

## KQL Download
KQL can be found [here](https://github.com/mattnovitsch/M365/blob/main/KQL/MDE/MDE-FindAccountsAddedtoGroup).