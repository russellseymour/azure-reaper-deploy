# Azure Reaper Deployment

This repository contains the ARM templates that are used to deploy the Azure Reaper into a subscription.

Full documentation for the deployment can be found in in the [Azure Reaper Deploy Documentation](https://chef-partners.github.io/azure-reaper-deploy).

Alternatively he documentation website can be run locally using Jekyll. To make thins even easier it can be run inside Docker using the following command

```powershell
docker run -it --rm -v "${PWD}/docs:/srv/jekyll" -p 4000:4000 -e JEKYLL_ENV=production jekyll/jekyll:3.8 jekyll serve
```

## Quick Start

To quickly deploy the Reaper and get up and running create a parameters file and use the following commands. (It is highly recommended that the documents are read and understood).

### Azure CLI

```bash
az group create -n Azure-Reaper -l westeurope
az group deployment create -g Azure-Reaper --template-uri https://raw.githubusercontent.com/chef-partners/azure-reaper/release/azuredeploy.json -p parameters.json
```

### PowerShell

```powershell
New-AzureRmResourceGroup -Name Azure-Reaper -Location westeurope
New-AzureRmResourceGroupDeployment -ResourceGroupName Azure-Reaper `
                                   -TemplateUri https://raw.githubusercontent.com/chef-partners/azure-reaper/release/azuredeploy.json `
                                   -TemplateParameterFile parameters.json
```

