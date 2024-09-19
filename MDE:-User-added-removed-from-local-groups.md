# Summary
I've seen the question asked a lot "How do I know if a user was added to a local group?". The answer is we detect and track that kind of information in Microsoft Defender for endpoint. The solution though is multi-part and has to take into account is the account being added local, Active Directory, and/or Entra.

## Solution
We don't keep track of accounts and SIDs for all the endpoints, just if there is activity with them such as a login or creation. In theory, if someone is adding an account to a group, they will more than likely be logging into it in a similar timeframe so between the three queries I have provided you should be able to get the SID and account name.
There were a couple of "gotchas" in the mix. 

* If the account is local, we wouldn't have a SID in Entra ID or On-prem AD to compare to.
* If the account was on-prem or Entra ID, the information for what the customer is looking for won't be available without MDI deployed.
* The identity information in the IdentityInfo table for the account doesn't match up to the SID column in the DeviceEvents table.
<BR> &emsp; a. DeviceEvents SID =AccountSid 
<BR> &emsp; b. IdentityInfo SID = CloudSID or OnPremSid

I came up with three different queries to resolve this issue.
 
The first one will find if a local account is created then added to a group. You can see from the screenshot that I was able to get the accounts that were recently created and added to groups.
![image](https://github.com/user-attachments/assets/d8d765c3-6dc2-4ad7-b9c9-9c0c2ed7bb94)

> //Find newly created local account added to group <BR>
DeviceEvents <BR>
| where ActionType contains "UserAccountAddedToLocalGroup" <BR>
| extend Fields=parse_json(AdditionalFields) <BR>
| extend AddToGroup = tostring(Fields.GroupName) <BR>
| extend GroupDomainName = tostring(Fields.GroupDomainName) <BR>
| join kind=inner (DeviceEvents <BR>
    | where ActionType contains "UserAccountCreated" <BR>
    | where AccountName <> "" <BR>
    | distinct AccountName, AccountSid <BR>
    ) on AccountSid <BR>
| extend InitiatedAction=strcat (InitiatingProcessAccountDomain, "\\", InitiatingProcessAccountName) <BR>
| project Timestamp, DeviceName, ActionType, InitiatedAction,AccountAdded=AccountName1, AddToGroup, GroupDomainName <BR>

The second query is looking for any cloud or on-prem account added to a group recently. Since we may not know when the account was created.
![image](https://github.com/user-attachments/assets/e0888470-53ea-4c96-af0a-8f6d2072d350)


> //Find cloud or on-prem accounts added to group <BR>
DeviceEvents <BR>
| extend placeholder=1 <BR>
| where ActionType contains "UserAccountAddedToLocalGroup" <BR>
| extend Fields=parse_json(AdditionalFields) <BR>
| extend AddToGroup = tostring(Fields.GroupName) <BR>
| extend GroupDomainName = tostring(Fields.GroupDomainName) <BR>
| join kind=inner (IdentityInfo <BR>
&emsp;    | extend placeholder=1 <BR>
&emsp;    | distinct AccountName, OnPremSid, CloudSid, placeholder <BR>
) on placeholder <BR>
| where AccountSid == OnPremSid or AccountSid == CloudSid <BR>
| extend InitiatedAction=strcat (InitiatingProcessAccountDomain, "\\", InitiatingProcessAccountName) <BR>
| project Timestamp, DeviceName, ActionType, InitiatedAction,AccountAdded=AccountName1, AddToGroup, GroupDomainName <BR>

The third query would tell you if the local account logged in and if it was recently added to a group.
![image](https://github.com/user-attachments/assets/563cf820-5d5b-40bf-8b91-c8d095979de9)

> //Find local account added to group  <BR>
DeviceEvents <BR>
//| where DeviceName contains "surface" <BR>
| where ActionType contains "UserAccountAddedToLocalGroup" <BR>
| extend Fields=parse_json(AdditionalFields) <BR>
| extend AddToGroup = tostring(Fields.GroupName) <BR>
| extend GroupDomainName = tostring(Fields.GroupDomainName) <BR>
| join kind=inner (DeviceLogonEvents <BR>
&emsp;    | where AccountName <> "" <BR>
&emsp;    | distinct AccountName, AccountSid <BR>
&emsp;    ) on AccountSid <BR>
| extend InitiatedAction=strcat (InitiatingProcessAccountDomain, "\\", InitiatingProcessAccountName) <BR>
| project Timestamp, DeviceName, ActionType, InitiatedAction, AccountAdded=AccountName1, AddToGroup, GroupDomainName, AdditionalFields <BR>

## Conclusion
This should cover most basis for finding when an account was either created on an endpoint from a newly created local account, your on-prem domain, your Entra environment, and/or a local account that was logged into.
