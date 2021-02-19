---
title: Tags
layout: default
nav_order: 40
---

# Tags
{: .no_toc }

Tags are used by the functions and people to set specific settings for resource groups.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

There are a number of tags that are used by Reaper. Three of them are added by the Reaper when a new resource group is created.

- `owner` - Name of the person that created the resource group.
- `ownerEmail` - Email address of the owner
- `createdDate` - Date the resource group was created in UTC

These are the only compulsory tags, without these Reaper will not work correctly.

For example the `createdDate` is used to determine when the group will expire. By default this is 7 days from the creation. The name and email address are used to illustrate who owns the group and for notification, if enabled.

## Optional Tags

There are a number of optional tags that can be applied to a resource group, either through the UI, the command line or something like Terraform.

### DAYSOFTHEWEEK
{: .label }

Default: 1,2,3,4,5

This specifies the days on which the virtual machines are permitted to run. The default is to run Monday to Friday where Sunday is day 0.

### InUse
{: .label }

Default: false

If Reaper is operating in a subscription where there are resources that need to be kept running without interruption, Reaper will ignore them if this tag is set.

### STARTSTOPTIME
{: .label }

Default: 0800-1800

So that virtual machines do not run when not being used, Reaper can shutdown and startup machines according to a schedule. By default this runs from 0800 to 1800, however this can be modified by using this tag.

The tag must be set in the form of `<START_TIME>-<STOP_TIME>`.

### TIMEZONE
{: .label }

Default: Virtual machine location

Reaper was designed to work with resources and teams across the world. By default it will determine the timezone to use from the location of the virtual machine. Thus if it is running in UK South it will use either UTC or BST depending on the time of year.

There maybe times when the virtual machine has to run in a different location but still be managed by Reaper on a different timezone. To achieve this the virtual machine can hae the `TIMEZONE` tag set.

## Examples

The following example shows how to change the tags on a resource group so that the machines are running on a Saturday and Sunday between 1200 and 2000.

### Bash

```bash
# Get the resource id to add the tag to
# In this example the command is getting the id to the resource group, but
# this could easily be a virtual machine
$id=`az group show -g rjs-test -query id -o tsv`

# Apply the new tags to the resource
az tag create --resource-id $id --tags DAYSOFTHEWEEK=6,0 STARTSTOPTIME=1200-2000
```

### PowerShell

```powershell
# Set the tags on the resource group
Set-AzResourceGroup -n rjs-test -tag @{ DAYSOFTHEWEEK="6,0", STARTSTOPTIME="1200-200"}

# In order to set the tags on a virtual machine, the id of that machine needs to be determined
$res = Get-AzResource -ResourceGroupName rjs-test -n rjs-vm
Set-AzResource -ResourceId $res.id -Tag @ { TIMEZONE="Eastern Standard Time" }
```