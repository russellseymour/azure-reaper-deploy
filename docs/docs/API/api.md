---
title: API
nav_order: 30
layout: default
has_children: true
---

# API
{: .no_toc }


## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

The application has an API endpoint that can be used to modify default settings and manage the subscriptions that Reaper will monitor and maintain.

There are 4 main endpoints in the API:

1. `/ops/setting/{id?}` - Get or set a specific setting
1. `/ops/location/{id?}` - Get or set a location for timezone calculations
1. `/ops/subscription/{id?}` - Get or set subscriptions that need to be managed
1. `/ops/reaper` - Force a run of reaper independent of the timer trigger