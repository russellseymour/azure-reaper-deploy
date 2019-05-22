---
permalink: /
layout: default
title: Overview
nav_order: 10
---

# Overview

This repository contains all of the templates that are required to deploy the Azure Reaper. It only concerns the deployment of the Reaper, if information about how the Reaper works and settings is required then please go to [Azure Reaper](https://chef-partners.github.io/chef-partners/azure-reaper).

When deploying the functions, the built in Continuous Delivery options in Azure Functions are utilised. This means that the code is tale from the `release` branch of `github.com/chef-partners/azure-reaper` by default. Whenever we update the code, all Azure Reaper instances that have been deployed using that will be updated to the code in that branch. If this is something that is not desired then please fork the Azure Reaper code so that updates only occur when required.

## Quick Start

{% include tip.html content="It is highly recommended that the documentation is read and understood before deploying the Reaper into an Azure subscription." %}

In order to to deploy the template a parameters file is required. The following shows an example of such a file:

{% markdown shared/parameters_file.md %}

The Reaper can be deployed using the defaults and thus no parameters, however it is expected that some taoliring is required for the environment that the Reaper will operate. Please refer to the [Deployment Parameters]({% link docs/parameters/parameters.md %}) for more information.

The following examples show how the templates can be deployed using either Azure CLI or PowerShell. It is assumed that the parameters file has been saved into the same directory as the command is being run from.

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