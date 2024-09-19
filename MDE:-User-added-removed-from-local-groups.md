# Summary
I've seen the question asked a lot "How do I know if a user was added to a local group?". The answer is we detect and track that kind of information in Microsoft Defender for endpoint. The solution though is multi-part and has to take into account is the account being added local, Active Directory, and/or Entra.

## Solution
There were a couple of "gotchas" in the mix. 

* If the account is local, we wouldn't have a SID in Entra ID or On-prem AD to compare to.
* If the account was on-prem or Entra ID, the information for what the customer is looking for won't be available without MDI deployed.
* The identity information in the IdentityInfo table for the account doesn't match up to the SID column in the DeviceEvents table.
<BR> &emsp; a. DeviceEvents SID =AccountSid 
<BR> &emsp; b. IdentityInfo SID = CloudSID or OnPremSid

I came up with two different queries. 
 
The first one will find if a local account is created then added to a group. You can see from the screenshot that I was able to get the accounts that were recently created and added to groups.
![image](https://github.com/user-attachments/assets/0095d9df-a091-4975-9132-e035a1d8c7a4)

> //Find newly created local account added to group <BR>
DeviceEvents <BR>
//| where DeviceName contains "surface" <BR>
| where ActionType contains "UserAccountAddedToLocalGroup" <BR>
| extend Fields=parse_json(AdditionalFields) <BR>
| extend AddToGroup = tostring(Fields.GroupName) <BR>
| extend GroupDomainName = tostring(Fields.GroupDomainName) <BR>
| join kind=inner (DeviceEvents <BR>
&emsp;    | where ActionType contains "UserAccountCreated" <BR>
&emsp;    | where AccountName <> "" <BR>
&emsp;    | distinct AccountName, AccountSid <BR>
&emsp;    ) on AccountSid <BR>
| project Timestamp, DeviceName, ActionType, AccountAdded=AccountName1, AddToGroup, GroupDomainName, AdditionalFields <BR>

This query is looking for any cloud or on-prem account added to a group recently. Since we may not know when the account was created.
![image](https://github.com/user-attachments/assets/de2215c7-7d32-4eed-8956-dfbb97c519ff)

> //Find cloud or on-prem accounts added to group <BR>
DeviceEvents <BR>
| extend placeholder=1 <BR>
//| where DeviceName contains "surface" <BR>
| where ActionType contains "UserAccountAddedToLocalGroup" <BR>
| extend Fields=parse_json(AdditionalFields) <BR>
| extend AddToGroup = tostring(Fields.GroupName) <BR>
| extend GroupDomainName = tostring(Fields.GroupDomainName) <BR>
| join kind=inner (IdentityInfo <BR>
&emsp;    | extend placeholder=1 <BR>
&emsp;    | distinct AccountName, OnPremSid, CloudSid, placeholder <BR>
) on placeholder <BR>
| where AccountSid == OnPremSid or AccountSid == CloudSid <BR>
| project Timestamp, DeviceName, ActionType, AccountAdded=AccountName1, AddToGroup, GroupDomainName, AdditionalFields <BR>
