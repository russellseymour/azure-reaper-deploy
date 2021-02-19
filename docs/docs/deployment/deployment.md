---
title: Deployment
nav_order: 20
has_children: true
layout: default
---

# Deployment
{: .no_toc }

This section describes how to use the ARM templates that are used to deploy the function into an Azure subscription.
{: .fs-6 .fw-300 }

---

When deploying the functions, the built in Continuous Delivery options in Azure Functions are utilised. This means that the code is tale from the `release` branch of `github.com/russellseymour/azure-reaper` by default. Whenever the code is updated, all Azure Reaper instances that have been deployed using that will be updated to the code in that branch. If this is something that is not desired then please fork the Azure Reaper code so that updates only occur when required.

Once the deploymenmt is complete the then the settings, timezones and subscriptions need to be uploaded.

## Customising the deployment

The quick start is good for getting things up and running, however there are a number of parameters that can be supplied when the ARM template is deployed.

The [Parameters](./parameters) page contains a list of the ones that can be specified.

## Deployment

{% include shared/deployment.md %}
