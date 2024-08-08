# Summary
In order to apply session or access policies in Defender for Cloud Apps you need to have a conditional access policy.

## Prerequisites
* Ensure your firewall configurations allow traffic from all the IP addresses listed on [Network requirements](https://learn.microsoft.com/en-us/defender-cloud-apps/network-requirements).
* Confirm that your application possesses a complete certificate chain. Incomplete or partial certificate chains may lead to unexpected behavior in applications when monitored with Conditional Access app control policies.

## Steps to deploy Conditional Access Application Policy

1. Navigate to [Entra Portal](https://entra.microsoft.com/)
2. Navigate to Protection > Conditional Access > Policies > New Policy
![image](https://github.com/user-attachments/assets/dd2d43de-ae3f-4344-8061-6b442683a9eb)
3. Give your policy a name for example "Conditional Access Application Control"
4. Apply users, I highly recommend using a test group that you can add users to for the POC or testing phase
5. Target resources: All Cloud Apps (or whatever applications you want to target
6. Session: Use Conditional Access App Control. I would engage you to leave the setting for Use custom policy as it will allow you to create more session and access policies. It will also give you more granular controls.
![image](https://github.com/user-attachments/assets/181492d1-414f-4232-907f-79bf38ff4550)
7. Test that this is working, simplest way I do it is just work for a day or two then navigate to [Defender XDR](https://security.microsoft.com)
8. Navigate to Settings > Cloud Apps > Connected Apps > Conditional Access App Control Apps. The applications will start to appear as you start access them from the accounts that you are sending through that conditional access policy. The more users will get your more applications faster but then you have a higher risk of applying policies prematurely. I would recommend you IT staff first so you can apply policies to just that group and test accordingly before expanding the test users.

![l0kjbmfj](https://github.com/user-attachments/assets/95781acb-1d14-4be8-9bea-eecbd1839d28)

## Next Steps
* [MDA ‐ Prevent Anonymous Proxies](https://github.com/mattnovitsch/M365/wiki/MDA-%E2%80%90-Prevent-Anonymous-Proxies)

## References
* https://learn.microsoft.com/en-us/defender-cloud-apps/conditional-access-app-control-how-to-overview