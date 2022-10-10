---
title: Journey Optimizer with Adobe Campaign Blueprint
description: Demonstrates how Adobe Journey Optimizer can be used with Adobe Campaign to natively send messages by utilizing the real-time messaging server in Campaign
solution: Journey Optimizer, Campaign, Campaign v8, Campaign Classic v7, Campaign Standard
exl-id: 076446a9-dfb9-464c-a04f-6864b8cb7b48
---
# Journey Optimizer with Adobe Campaign

Demonstrates how Adobe Journey Optimizer can be used with Adobe Campaign to natively send messages by utilizing the real-time messaging server in Campaign.

<br>

## Architecture

<img src="assets/ajo-campaign-architecture.svg" alt="Reference architecture Journey Optimizer blueprint" style="width:100%; border:1px solid #4a4a4a" />

>[!IMPORTANT]
>Using both Journey Optimizer and Campaign to send messages independently of each other is possible but has some technical considerations that need to be thought through. If you wish to pursue this route please work with your Pre-Sales Enterprise Architect to ensure that you have an understanding of what will be required to support the implementation.

<br>

## Prerequisites

### Adobe Experience Platform

* Schemas and datasets must be configured in the system before you can configure Journey Optimizer data sources
* For Experience Event class-based schemas add 'Orchestration eventID field group when you want to have an event triggered that is not a rule-based event
* For Individual Profile class-based schemas add the 'Profile test details' field group to be able to load test profiles for use with Journey Optimizer
* Journey Optimizer and Campaign are provisioned in the same IMS Org

### Campaign v7/v8 or Campaign Standard

* Execution instance of the real-time messaging service (i.e Message Center) must be hosted by Adobe Managed Cloud Services
* All message authoring is done within the Campaign instance itself

<br>

## Guardrails

[Journey Optimizer Guardrails Product Link](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=en)

### Additional Journey Optimizer Guardrails

* Capping is available via API today to ensure that the destination system is not saturated to the point of failure. This means that messages that exceed the cap will be dropped completely and never sent. Throttling is not supported.
  * Max connections - maximum number of http/s connections a destination can handle
  * Max call count - maximum number of calls to be made in the periodInMs paramater
  * periodInMs - time in milliseconds
* Segment membership initiated journeys can operate in two modes:
  * Batch segments (refreshed every 24hrs)
  * Streaming segments (<5mins qualification)
* Batch segments – need to ensure you understand the daily volume of qualified users and ensure the destination system can handle the burst throughput per journey and across all journeys
* Streaming segments – need to ensure the initial burst of profile qualifications can be handled along with the daily streaming qualifying volume per journey and across all journeys
* Decision Management in not supported
* Business events are not supported
* Outbound integrations to 3rd Party systems
  * No support for a single Static IPs as our infrastructure is multi-tenant (must allow list all datacenter IPs)
  * Only POST and PUT methods are supported for custom actions
  * Authentication support: token | password | OAuth2
* No ability to package and move individual components of Adobe Experience Platform or Journey Optimizer between various sandboxes. Must re-implement in new environments

<br>

### Campaign Integrations

For guidance on integration with your specific version of Adobe Campaign and Adobe Journey Optimizer, please see the corresponding guide for each Adobe Campaign Version.

* [Adobe Journey Optimizer & Campaign v7](ajo-and-campaign-v7.md)
* [Adobe Journey Optimizer & Campaign v8](ajo-and-campaign-v8.md)