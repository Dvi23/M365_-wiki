# Summary
I had a request from one of my customers to remove old guest accounts that he had from a CSV file provided by another team. He wanted to know how to get the UPNs so he could remove the accounts. I first tried doing this through Get-AzureADUser but that was not allowing me to use the variables in the filters. I found a support article that had something similar to what I wanted so I expanded upon it with what I was trying to do. The script now imports your csv as the source of your filter. Then checks your Azure AD using Get-MSOLUser and puts all the UserPrincipalName(UPN) in an array. In this instance the customer had received a list from his partner on employees that were no longer working on the project. This is the alternative email address field in the system, that is what I used for the example but you can change it to whatever you have available.

## Reference
* [Kevin Morgan](https://techcommunity.microsoft.com/t5/office-365/get-msoluser-filtered-variable/m-p/353898)

## Steps
1. Download [DeleteGuestAccounts.ps1](https://github.com/mattnovitsch/M365/blob/main/DeleteGuestAccounts.ps1).
2. Open DeleteGuestAccounts.ps1 in PowerShell ISE from the machine you plan to run the script from.
3. Edit line 3 to reflect the location of your download file. I had mine in a random folder on my C drive. <BR>
![](https://github.com/mattnovitsch/M365/blob/main/DeleteGuestAccounts/DGA1.jpg)
4. Execute the entire script
* Note: The script doesn't remove accounts by default, that part is commented out.
![](https://github.com/mattnovitsch/M365/blob/main/DeleteGuestAccounts/DGA2.jpg)
5. Once you verify all the accounts are correct and you are fine with deleting them. Delete the # on line 12.
6. Execute the script again to delete the accounts.

## Safety net
If you delete some accounts that you didn't want to or need to recover some run the below in PowerShell ISE, you just have to put the UPN between the double quotes.

Restore-MsolUser -UserPrincipalName ""