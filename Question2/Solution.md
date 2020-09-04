Q2 - SCENARIO
Macro Life, a healthcare company has recently setup the entire Network and Infrastructure on Azure. 
The infrastructure has different components such as Virtual N/W, Subnets, NIC, IPs, NSG etc.
The IT team currently has developed PowerShell scripts to deploy each component where all the properties of each resource is set using PowerShell commands.
The business has realized that the PowerShell scripts are growing over period of time and difficult to handover when new admin onboards in the IT.
The IT team has now decided to move to ARM based deployment of all resources to Azure.
All the passwords are stored in a Azure Service known as key Vault. The deployments needs to be automated using Azure DevOps using IaC(Infrastructure as Code).

1) What are different artifacts you need to create - name of the artifacts and its purpose
2) List the tools you will to create and store the ARM templates.
3) Explain the process and steps to create automated deployment pipeline. 
4) Create a sample ARM template you will use to deploy a Windows VM of any size
5) Explain how will you access the password stored in Key Vault and use it as Admin Password in the VM ARM template.

Solution:
1)	Artifacts can be created for each Azure resource which contain the template.json and parameters.json file for the specific Azure Resource.

2)	ARM templates can be created using VS code and can be stored under Github Repository and there are multiple Externsions available in VSCode.

3)	Under Azure Devops Portal open the Project  and create New Pipeline. Select  use a visual designer option.
•	On the new pane, select deploy and click on Azure Resource Group deployment and click ADD.
•	On the left pane, select Azure Deployment: Create or Update Resource Group action on
•	Select Azure Subscription and click on Authorize.
•	Select your resource group on your Azure subscription and location.
•	The template location will be linked artefact.
•	Select your template file (azuredeploy.json) from the selection menu.
•	Select your template parameter file (azuredeploy.parameters.json) from the selection menu.
•	Deployment mode: complete.
•	Click save and queue and provide your comment on the file changes.
•	After it  has saved, the build operation will commence deployment  on your Azure tenant.
•	You can view the deployment logs from the Azure DevOps portal. In addition, you will receive an email (email which has been used for Azure DevOps account) with deployment status.
•	Verify your network (Azure Resource which we added on ARM template) has been created on Azure tenant.
•	Now, the next step is to enable continuous integration. Which will keep your build updated based on your changes on project / ARM templates.
•	Select Builds on the left pane and click pipeline, which you have created. Click on Edit.
•	Click on Triggers and select Enable continuous integration. Click on Save.

4)	ARM template is stored under https://github.com/nitinpokharna/Assignment/Question2/template.json

5)	When we need to provide the value of parameter Admin password from key vault the reference of keyvault to be added in the ARM template
For Example:

"adminPassword": {
"reference": {
"keyVault": {
		"id": "/subscriptions/{subscription-guid}/resourceGroups/{keyvault-rg}/providers/Microsoft.KeyVault/vaults/ProvisioningVault"
		},
"secretName": "AdminPass"
}
}
