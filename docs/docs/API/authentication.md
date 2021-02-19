---
title: Authentication
parent: API
layout: default
---

# Authentication

When accessing the API, authentication is required. This has to be set on the request using the `x-functions-key` header value. This value can be retrieved using the Azure Portal or from the command line using the Key Management API.

## Azure Portal

To get this navigate to the deployed application in the portal and select 'App Keys' from the left hand navigation.

![Function App Key](/images/function-app-key.png)

## Command Line

It is possible to use the `az` command line utility to retrieve the key for the function, however this will _only_ return the master key for the function.

_The following code snippet assumes a function name of `azure-reaper` in the `Azure-Reaper` resource group_.

```bash
az functionapp -n azure-reaper -g Azure-Reaper -o table
```

This will return the master key for the function.

```
MasterKey
--------------------------------------------------------
y8QqYgnAIas8Dyp9nUcNhwoc3lalIadhdvIGSEJlbdRLmn4fjFprjyg==
```