---
permalink: /
layout: default
title: Overview
nav_order: 10
---

# Azure Reaper
{: .no_toc }

Azure Reaper is an Azure function that helps to manage resources in Azure. Using a tagging system is will shutdown and startup machines and delete them after an expiration period.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

The Azure Reaper has been designed to help with the management of costs within an Azure subscription. It does this by focusing on reducing the time that Virtual Machines are actively running, e.g. the time that they are needed. It will also ensure that resources are not left around to run indefinitely.

When a new resource group is created the Reaper will use the event information to automatically tag the resource group with an owner, an email address and the creation date.

![Tagged Resource Groups](/images/tagged_resource_groups.png)

The automatic tagging of a resource group is necessary as Azure does not provide this information when a resource group is interrogated.

Once the Reaper is enabled for a subscription it will perform the following tasks:

 - shutdown and startup machines according to a specified time window
 - removal of resource groups after an expiration time, default of 7 days

Production resource groups can be protected against being reaped by using another tag - `inUse`. By default, if the default settings are used, virtual machines are able to run between 0800 and 1800 Monday to Friday. This can be modified using more tags and can be set to work with other timezones.
## Quick Deployment

{% include shared/deployment.md %}
