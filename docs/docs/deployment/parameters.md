---
title: Parameters
nav_order: 20
layout: default
parent: Deployment
---

# Parameters
{: .no_toc }

There are a few parameters that can be used to affect the way in which the Azure Reaper function is deployed into Azure.
{: .fs-6 .fw-300 }

---

The following table details the parameters that can be specified when deploying the Azure Reaper.

| Name | Description | Default Value |
|---|---|---|
| `prefix` | Prefix that will be applied to all Azure Reaper resources. This is so that multiple instances can be deployed if required | AZReaper |
| `spTier` | App Service plan tier that should be used | Standard |
| `spName` | Name of the service plan to use | S1 |
| `spSize` | Size of the service plan to use | S1 |
| `spFamily` | Family code of the resource SKU | S |
| `spCapacity` | Default number of workers for this app | 1 |
| `autoDiscoverSASToken` | State if the template should try to auto discover the SAS token from the deployment. This is used when building and testing the template in Azure DevOps. | false |
| `azureStorageSASToken` | SAS token that has been generated if the templates are to be read from azure table storage | null |
| `reaperRepoUrl` | Repository URL for the Reaper code | [{% include replacements/reaper_base_repo_url.txt %}]({% include replacements/reaper_base_repo_url.txt %}) |
| `reaperRepoBranch` | Branch that the code should be deployed from | release |
| `baseUrl` | Base URL from which nested templates can be retrieved | null |
| `uniqueShort` | A string of 4 or 5 characters that will be used to help uniquely identify the resources that are created. If this is not specified then a value will be automatically created. | null |

## Base URL

The templates are designed to be deployed using the `az` command line tool with the `--templateLink` option. The value that is used for this file is used to work out the URL for the nested templates that are required for the build.

However sometimes it maybe necessary to deploy the main template from the local machine. In this case the `baseUrl` parameter is required so that `az` can find the templates to deploy.