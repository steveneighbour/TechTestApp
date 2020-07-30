# Results Documentation

This github repo and associated action deploys the demo TechTestApp application to Azure Container Instances (ACI). I initially was going to use Azure Devops for this but the brief indicated github should drive the deployment.  This means i switched to using Github Actions.

ACI was chosen for speed of implementation + meeting the brief of "do not over engineer".  It doesn't allow for auto-scaling, but this could easily be addressed given more time by adding more container instances + adding an Application Gateway.  We'd also then include TLS, Azure log analytics, AppInsights monitoring etc etc.

### PreRequisites
  - Create a new Azure Resource Group called techtestapp-rg
  - Add tags to Resource Group, to allow for auditing and ownership allocation
  - Create a ServicePrincipal
```az ad sp create-for-rbac --name "techtestapp-sp" --role contributor  --scopes /subscriptions/{subscriptionid}/resourceGroups/techtestapp-rg --sdk-auth```

### Build
  - For speed of implementation, i cloned the demo docker repo to https://github.com/steveneighbour and setup a docker autobuild via docker hub
  - Docker file is accessibile here https://hub.docker.com/repository/docker/sneighbour/techtestapp

### Release
  - Github Actions was used, to deploy the TechTestApp and associated postgresdb containers to ACI
  - All parameters are stored as Github secrets

ARM Template is located here - https://github.com/steveneighbour/TechTestApp/blob/master/deploy/azuredeploy.json

Azure Screenshots

![Containers](https://github.com/steveneighbour/TechTestApp/raw/master/deploy/containers.png)
![Container Group](https://github.com/steveneighbour/TechTestApp/raw/master/deploy/containergroup.png)

Github Action Screenshot

![Swagger](https://github.com/steveneighbour/TechTestApp/raw/master/deploy/githubaction.png)


### End Result

![HomePage](https://github.com/steveneighbour/TechTestApp/raw/master/deploy/homepage.png)


![Swagger](https://github.com/steveneighbour/TechTestApp/raw/master/deploy/swagger.png)

Website is accessible here;

http://techapptest1234xxx.australiaeast.azurecontainer.io

http://techapptest1234xxx.australiaeast.azurecontainer.io/swagger/

Please let me know when i can tear down the Azure resources
