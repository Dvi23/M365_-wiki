# Summary
I have been asked to exclude a group from patching for a month by a few customers while they run end of year reporting in their finance departments. This can be done several different ways, but the important thing is to make sure your organization signs off on the change. What I have done is permanently set a group in Microsoft Endpoint Manager as exclusion group. In this case, I created a ExlusionGroup and FinanceDevices groups. I will be automating the FinanceDevices group to be added to the ExclusionGroup based on the month and removing the following month.

## Prerequisite
* AddgrouptoExclusionGroup.ps1
* Using Power Automate or some other tool that allows you to run jobs on a schedule

## Steps
1. Navigate to the [MEM Portal](https://endpoint.microsoft.com/)
2. Navigate to Tenant Administration then select Roles <BR>
![image](https://user-images.githubusercontent.com/61195587/165753017-5d025579-1bae-46f9-a13f-2a7d4e8c5495.png)
3. Select Scope(Tags), click Create <BR>
![image](https://user-images.githubusercontent.com/61195587/165753230-706a7ab9-359b-455b-95f0-f2516d9be13d.png)
4. Name your group, for my example we are calling them Finance Devices, select Next to continue
![image](https://user-images.githubusercontent.com/61195587/165753715-e35b6dda-737e-4946-bb31-97731b8cebb0.png)
5. Clcik Add Groups, in the search box type the name of your group. Double click it then click select <BR>
![image](https://user-images.githubusercontent.com/61195587/165753978-bfbc1dca-b87d-4d79-bd8d-1b5049428b58.png)
6. Select Next to proceed <BR>
7. Click Create <br>
![image](https://user-images.githubusercontent.com/61195587/165754608-e9e9ac2c-fc8c-4b8d-8400-38e4229494fe.png)
8. Navigate to Tenant Administration > Filters then click create <BR>
![image](https://user-images.githubusercontent.com/61195587/165758203-3113335d-df84-4d89-97c0-17fa31b57f16.png)
9. Name the filter, for my example we will call it financedevices, Select the platform to Windows 10 and later then click next <BR>
![image](https://user-images.githubusercontent.com/61195587/165758513-30d78f2f-c308-40ae-aa4b-4e9ac94722fc.png)
10. 
