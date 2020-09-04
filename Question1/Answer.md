Q1 - SCENARIO
A car rental company called FastCarz has a .net Web Application and Web API which are recently migrated from on-premise system to Azure cloud using Azure Web App Service
and Web API Service.
The on-premises system had 3 environments Dev, QA and Prod.
The code repository was maintained in TFS and moved to Azure GIT now. The TFS has daily builds which triggers every night which build the solution and copy the build package to drop folder.
deployments were done to the respective environment manually. The customer is planning to setup Azure DevOps service for below requirements:

1) The build should trigger as soon as anyone in the dev team checks in code to master branch.
2) There will be test projects which will create and maintained in the solution along the Web and API. The trigger should build all the 3 projects - Web, API and test.
   The build should not be successful if any test fails.
3) The deployment of code and artifacts should be automated to Dev environment. 
4) Upon successful deployment to the Dev environment, deployment should be easily promoted to QA and Prod through automated process.
5) The deployments to QA and Prod should be enabled with Approvals from approvers only.

Explain how each of the above the requirements will be met using Azure DevOps configuration.
Explain the steps with configuration details.


Solution

1)	Under Trigger tab in Build pipeline select continuous integration and select the branch filters as Master.
2)	Create 3 different Pipelines for all 3 projects. .Net core task in the Build pipeline can be used to run unit tests and once the unit test are successful the task for build and package the code can be executed.
3)	To automate the deployment of code and artifact under Dev environment release pipeline can be linked to the Dev artifact and Continuous deployment trigger to be enabled in the Dev Environment linked to the artifact.
4)	Stage trigger is used for this purpose. A linear pipeline is created for this purpose in which release is first deployed in Dev  stage and once it is succeed, it will deploy to QA and then to Prod.
5)	In the Pipeline choose Pre Deployment conditions in the stages section and scroll down to pre deployment approvers and enable it. In the Approvers section, users can be selected from the list. 
