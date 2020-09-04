Q3 - SCENARIO
A Toy Retail company ToyTrex has it retail application deployed as 3-tier application - Web App(UI), Web API(middle layer) and Database as Azure SQL.
The user load started increasing multiple fold every month and complex programs getting implemented, the application started performing poorly.
As a result, company decided to re-architect the middle layer as microservices using Azure Kubernetes Services.
The new architecture has below design decisions.

1) The middle layer should be implemented as Microservices using Azure AKS
2) The middle layer API should be deployed as containerized application images
3) The container images will use Azure Container Repository (ACR) as the private image repository
4) The CI/CD pipelines for microservices should be implemented using Azure DevOps services.
5) The Azure DevOps should be able to access ACR and download the container images for microservices deployment
6) The image should be deployed as templates such as <image_name>:<build_id>

Explain the DevOps configuration and steps in detail for above requirements

Solution:
1)	AKS Cluster to be setup with minimum One node cluster
2)	Create docker file for API application to convert Containerized application image.
3)	The Build and Release pipeline to be created in following Manner:

 
Under  Build pipeline 
Click on Create pipeline using YAML or Classic editor, choose Docker template
    Build an image
    Push image to ACR
    Action: Build an image
    Select Dockerfile location
    Image Name: $(Build.Repository.Name):$(Build.BuildId)
    Install Helm Packages for Deployment
    Push an image
    Copy ARM Template
    Create Artifact
    ARM template 


 
Under Release pipeline Select the Arm templated created from Build and deploy the images.
    New release pipeline
    Slect Deploy to kuberentes cluster
    Extract  Resource Information ( Powershell)
    Kubectl create namespace
    Kubectl set ImagePullSecrets
    Intall Helm 
