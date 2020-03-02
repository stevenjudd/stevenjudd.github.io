---
layout: post
title: Why Learn To Automate
---

If you are trying to justify to your organization's management that using PowerShell to automate tasks is a worthwile effort,
look at the following example where I used PowerShell to automate an application deployment task.
The first table is the actual process and the second table is the value of the automation.

Below is a comparison of the process the Web Application Administrators used to use for deploying a .NET web application to an internal web server.
I have anonymized some of the information to make the process more generic:

|Manual|Scripted|
|---|---|
|Open Service Request containing the request for deployment|Open Service Request containing the request for deployment|
|Click on link to open Configuration Management tool (CMTool)|Click on link to open Configuration Management tool (CMTool)|
|Search the Push ID in the Service Request and click the link|Search the Push ID in the Service Request and click the link|
|Click on the Accept button|Click on the Accept button|
|Open Xplorer2 as Admin account|Open PowerShell as Admin account|
|**Create** the path in the Admin Code Vault for the **projectName**, **CodeType**, and **Version** following the path format of \\\server\share$\codeVault\admin\\[projectName]\\[codeType]\\[version] where projectName is a valid directory name from the Project field of CMTool, codeType is the type of code solution being deployed from the Code Type field of CMTool, and version is from the Build # field of the CMTool.|Run “Install-dvnCMCode -PushID [**Record ID**]” where Record ID is from the CMTool.|
|**Copy** all the files from the Build Directory field in the CMTool to the Admin Code Vault location|Review the source and destination directories, project name, and code type and if correct press Enter. Otherwise, enter N and press Enter to exit the deployment.|
|**Copy** all the files from the Admin Code Vault path **except** the .config files|..|
|Get the Destination Path from the CMTool and open in Xplorer2. Paste the copied files to the destination. If the destination does not exist, **create** the destination path before copying.|..|
|Open BeyondCompare as Admin account|Open BeyondCompare as Admin account|
|Run a compare against the source and destination looking for orphaned files and changed .config files. **Update** .config files as directed in the CMTool General Changes comment section|Run a compare against the source and destination looking for orphaned files and changed .config files. **Update** .config files as directed in the CMTool General Changes comment section|
|Return to CMTool and mark the deployment as “deployed as instructed”|Return to CMTool and mark the deployment as “deployed as instructed”|
|Return to Service Request and complete and close the request|Return to Service Request and complete and close the request|

**Note**: The bolded text in the table above is a manual data entry step, which is a location where an error could be introduced to the deployment process.
As you can see, there are many locations where the manual process has an opportunity for an error to occur.
With the scripted release, you don’t have to worry about whether you copied the config files to the vault yet did not copy them to the destination.
It handles that for you.

Also, there is only one place where you can enter bad data,
and the Review step allows you to easily correct that before deploying.

Finally, with the scripted process, the developer receives an email with the results of the script when the deploy is complete.
They know immediately when the deploy can be tested and can review all the files deployed without requiring an admin to be involved.
This also means a faster turn around time. This log of the activity is also copied to a deployment repository for history and review if required.
This log could be obtained from the manual process, but it would require even more steps, more time, and more opportunity for errors.

The accuracy of and notification from the automated release is its primary value, however it is also anywhere from 5 to 10 minutes faster considering the actions it completes. I wrote the initial version in 2012 and added the logging in 2013.
Here are the numbers of code deployment releases by year, the estimated time saved in minutes on the low side and high side, and the low dollar cost based on a $50/hour contractor and the high dollar cost based on a $100/hour full time employee (these values are somewhat arbitrary but make the math easy):

|Year|Release Count|Low Time|High Time|Low $|High $
|---|---|---|---|---|---|
2013|93|465|930|$387.50 |$1,550.00|
2014|307|1535|3070|$1,279.17 |$5,116.67|
2015|724|3620|7240|$3,016.67 |$12,066.67|
2016|1099|5495|10990|$4,579.17 |$18,316.67|
2017|842|4210|8420|$3,508.33 |$14,033.33|
2018|445|2225|4450|$1,854.17 |$7,416.67|
2019|145|725|1450|$604.17 |$2,416.67|
Total|3655|18275|36550|$15,229.17 |$60,916.67|

Remember, this chart is an estimation of the time and money saved.
It does not calculate the time and money lost from any errors from the manual process.

**Note**: we have moved from the internal release script to VSTS/AzDO for our automated releases, so the number of releases per year has begun to decline.

The point of automation may or may not be time savings.
It may be purely to ensure a process is followed precisely and accurately.
However, I would submit that almost every automation saves some time, and since time has a cost, it also saves money. 