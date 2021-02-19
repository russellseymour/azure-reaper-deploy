{% include tip.html content="It is highly recommended that the documentation is read and understood before deploying the Reaper into an Azure subscription." %}

In order to to deploy the template a parameters file is required. The following shows an example of such a file:

{% include shared/parameters_file.md %}

The Reaper can be deployed using the defaults and thus no parameters, however it is expected that some tailoring is required for the environment that the Reaper will operate. Please refer to the [Deployment Parameters]({% link docs/deployment/parameters.md %}) for more information.

The following examples show how the templates can be deployed using either Azure CLI or PowerShell. It is assumed that the parameters file has been saved into the same directory as the command is being run from.

### Azure CLI

```bash
az group create -n Azure-Reaper -l westeurope
az group deployment create -g Azure-Reaper --template-uri {% include replacements/reaper_base_repo_url_raw.txt %}/release/azuredeploy.json -p parameters.json
```

### PowerShell

```powershell
New-AzureRmResourceGroup -Name Azure-Reaper -Location westeurope
New-AzureRmResourceGroupDeployment -ResourceGroupName Azure-Reaper `
                                   -TemplateUri {% include replacements/reaper_base_repo_url_raw.txt %}/release/azuredeploy.json `
                                   -TemplateParameterFile parameters.json
```

## Configuration

Once the deployment has been completed, reaper needs to be configured with [Settings](/docs/deployment/settings) and [Subscriptions](/docs/deployment/subscriptions).