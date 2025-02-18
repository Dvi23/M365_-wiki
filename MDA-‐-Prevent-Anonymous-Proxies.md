# Summary
Even having a geo-fence in your environment is not enough anymore. Attackers are using Anonymous Proxies to jump the geo-fence and attack environments. To help prevent that, you can block those proxies using Microsoft Defender for Cloud Apps.

## Perquisites
You must have a [Conditional Access Application Control](https://github.com/mattnovitsch/M365/wiki/MDA-%E2%80%90-Conditional-Access-Application-Control) policy deployed.

## Steps to enable the block of the proxies.

1. Navigate to [Microsoft Defender XDR](https://security.microsoft.com).
2. Navigate to Cloud Apps > Policies > Policy Management
3. Select Create Policy > Access Policy
![f4xur1ha](https://github.com/user-attachments/assets/db945793-2ccc-4269-a02e-c55482c4e8f8)

<BR>
4. Enter the policy name, for example "Prevent Anonymous Proxies" <BR>
5. Under Activities matching all of the following, I would suggest you delete device and App <BR>
6. Add IP Address > Tag > equals > Anonymous Proxy <BR>
7. Under Actions select Block <BR>
* Note: Feel free to add a custom message to this block <BR>
8. I would strongly recommend turning off Alerts for this policy so you are not spammed with alerts that you would just have to close. You can do reporting data in Advance Hunting if you want to see the data.

![image](https://github.com/user-attachments/assets/e7b869e9-8baf-4136-aa74-5c3150e15585)



