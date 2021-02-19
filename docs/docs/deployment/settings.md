---
title: Settings
layout: default
nav_order: 30
parent: Deployment
---

# Settings
{: .no_toc }

Reaper depends on a few settings. All of the settings are stored in the backend CosmosDB database, and some of them can be overridden by tags on the resource.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text_delta }

1. TOC
{:toc}

---

## Upload API Settings

Once the deployment has been completed the Reaper needs to be configured with some default settings.  A lot of these settings can be overridden using the user tags, but when these do not occur on a resource group there has to be a value that Reaper can use.

The main `{% include replacements/reaper_base_repo_url.txt %}` repository has two files which contain the default values for the settings and the timezones.

1. {% include replacements/reaper_base_repo_url_raw.txt %}/master/data/settings.json
1. {% include replacements/reaper_base_repo_url_raw.txt %}/master/data/timezones.json

In order to access the API, the function key needs to be retrieved, please refer to the [API Authentication](/docs/API/authentication/) page for more information.

The easiest way to upload the necessary items is to use the command line. The following examples show how this can be done using both `curl` and `powershell`.

{% include note.html content="In both cases a dummy API token is being used for the authentication. The URL for the Azure Reaper endpoint will depend on where the function was deployed to and the parameters that were used" %}

### Curl

```bash
# Download the two files to the local machine
curl {% include replacements/reaper_base_repo_url_raw.txt %}/master/data/settings.json -o settings.json
curl {% include replacements/reaper_base_repo_url_raw.txt %}/azure-reaper/master/data/timezones.json -o timezones.json

# Upload the settings to the API
curl -H "x-functions-key: functiontoken123!" \
     -X POST \
     -d @settings.json \
     https://azure-reaper.azurewebsites.net/ops/settings

# Upload the timezones to the API
curl -H "x-functions-key: functiontoken123!" \
     -X POST \
     -d @timezones.json \
     https://azure-reaper.azurewebsites.net/ops/timezones
```

### PowerShell

```powershell
# Download the two files to the local machine
Invoke-RestMethod -Uri {% include replacements/reaper_base_repo_url_raw.txt %}/master/data/settings.json -OutFile settings.json
Invoke-RestMethod -Uri {% include replacements/reaper_base_repo_url_raw.txt %}/master/data/timezones.json -OutFile timezones.json

# Upload the settings to the API
Invoke-RestMethod -Method POST `
                  -Headers @{"x-functions-key": "functiontoken123!"} `
                  -Body (Get-Content -Path settings.json -raw) `
                  -Uri https://azure-reaper.azurewebsites.net/ops/settings

# Upload the timezones to the API
Invoke-RestMethod -Method POST `
                  -Headers @{"x-functions-key": "functiontoken123!"} `
                  -Body (Get-Content -Path timezones.json -raw) `
                  -Uri https://azure-reaper.azurewebsites.net/ops/timezones

```