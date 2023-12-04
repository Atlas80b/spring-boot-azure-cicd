# Azure Web App deployment pipeline with Github Actions
This repository contains 2 simple implementations of a pipeline that creates automatic deployments to an Azure Web App whenever code is pushed to a specifc branch (`dev` in this case).

## Private Web App 
In case the Azure Web App is using a private endpoint and it is not publicly available, the deployment strategy consists of uploading the jar file to an Azure Storage Container.  
Through the Azure CLI the web app pulls the jar file using a generated SAS URL and deploys it.  
More details available in [this blog post](https://azure.github.io/AppService/2021/03/01/deploying-to-network-secured-sites-2.html).

- Workflow file: `deploy-webapp-private-endpoint.yml`

## Public Web App 
In case of a publicly available Web App, then the deployment strategy is pretty straightforward and simply uses [azure/webapps-deploy@v2](https://github.com/Azure/webapps-deploy).  
- Workflow file: `deploy-public-webapp.yml`

### Notes:
This repository assumes that the Azure Subscription where the app resides has a proper role assignment for the Service Principal responsible to run the workflows.
More specifically the authentication mechanism is done via [OpenID Connect](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/guides/service_principal_oidc).

OIDC setup example: https://github.com/jongio/github-azure-oidc
