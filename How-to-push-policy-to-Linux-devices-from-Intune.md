## Summary
Now that we have onboarded devices with Microsoft Defender for Endpoint, we need a way to manage the policy. We could do it locally but that becomes a pain for large scale. You best option is using management tools like Intune, chef, puppet. As I am not a Linux guru, but I know Intune we will focus on that route here.

* **Note: As of today the method that this page will be outlining will not work for GovCloud customers**

## Deployment steps

1. Go to [Defender XDR](https://security.microsoft.com)
2. Navigate to Settings > Endpoints > Enforcement Scope
3. We need to turn on Use MDE to enforce security configuration settings from Intune
4. We then need to turn on the Linux Device slider. If you only onboarded a few test devices, setting the radio button to "On All Devices" will work. If you have already onboarded all your devices then I would recommend using "On Tagged Devices"
* Note: If you select "On Tagged Devices", you will need to manually tag the devices you want to be managed with a tag of "MDE-Management"
![image](https://github.com/mattnovitsch/M365/assets/61195587/9468fb2e-edb7-4b9c-9ac4-f55ea16ec848)

5. Save the page at the bottom.
6. Go to [Entra](https://entra.microsoft.com/)
7. Navigate to Groups > All groups then select New group
![image](https://github.com/mattnovitsch/M365/assets/61195587/edaf8610-1f2e-4d65-875a-1f976bc91271)

8. Enter a group name and change membership type to Dynamic Device, then click Add dynamic query
* Note: If you want to add specific set of devices then name appropriately
![image](https://github.com/mattnovitsch/M365/assets/61195587/e1e9e91f-f35d-4c66-b079-952499e74348)

9. 
6. Navigate to Endpoints > Endpoint Security Policies > Linux Policies and select Create New Policy 
![image](https://github.com/mattnovitsch/M365/assets/61195587/e9937dac-21ff-44b1-abae-fe1849ae03e8)

7. Select Linux as the Platform and Select Microsoft Defender Antivirus as the Template
* Note: If you need separate exclusions for different server groups, I would recommend creating exclusions and deploy to specific groups to not blank exclude processes.
![image](https://github.com/mattnovitsch/M365/assets/61195587/7d631364-dc72-44f8-9387-5675c8339c7a)
