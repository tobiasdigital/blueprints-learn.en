---
title: Journey Optimizer - 3rd Party Messaging Blueprint
description: Demonstrates how Adobe Journey Optimizer can be utilized with 3rd party messaging systems to orchestrate and send personalized communications.
solution: Experience Platform, Journey Optimizer
exl-id: 3a14fc06-6d9c-4cd8-bc5c-f38e253d53ce
---
# 3rd Party Messaging

Demonstrates how Adobe Journey Optimizer can be utilized with 3rd party messaging systems to orchestrate and send personalized communications.

<br>

## Architecture

<img src="assets/3rd-party-messaging-architecture.svg" alt="Reference architecture Journey Optimizer blueprint" style="width:100%; border:1px solid #4a4a4a" />

<br>

## Prerequisites

Adobe Experience Platform

* Schemas and datasets must be configured in the system before you can configure Journey Optimizer data sources
* For Experience Event class-based schemas add 'Orchestration eventID field group when you want to have an event triggered that is not a rule-based event
* For Individual Profile class-based schemas add the 'Profile test details' field group to be able to load test profiles for use with Journey Optimizer

3rd Party Messaging Application

* Must support REST API calls for sending transactional payloads

<br>

## Guardrails

[Journey Optimizer Guardrails Product Link](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=en)

Additional Journey Optimizer Guardrails: 

* Capping is available via API today to ensure that the destination system is not saturated to the point of failure. This means that messages that exceed the cap will be dropped completely and never sent. Throttling is not supported.
  * Max connections - maximum number of http/s connections a destination can handle
  * Max call count - maximum number of calls to be made in the periodInMs paramater
  * periodInMs - time in milliseconds
* Segment membership initiated journeys can operate in two modes:
  * Batch segments (refreshed every 24hrs)
  * Streaming segments (<5mins qualification)
* Batch segments – need to ensure you understand the daily volume of qualified users and ensure the destination system can handle the burst throughput per journey and across all journeys
* Streaming segments – need to ensure the initial burst of profile qualifications can be handled along with the daily streaming qualifying volume per journey and across all journeys
* Offer Decisioning in not supported
* Outbound integrations to 3rd Party systems
  * No support for a single Static IPs as our infrastructure is multi-tenant (must allow list all datacenter IPs)
  * Only POST and PUT methods are supported for custom actions
  * Authentication support: token | password | OAuth2
* No ability to package and move individual components of Adobe Experience Platform or Journey Optimizer between various sandboxes. Must re-implement in new environments

<br>

3rd Party Messaging System

* Need to understand what load the system can support for transactional API calls
  * Number of calls allowed per second
  * Number of connections
* Need to understand what authentication is required to make API calls
  * Auth type:  token | password | OAuth2 are supported via Journey Optimizer
  * Auth cache duration:  how long is the token valid? 
* If batch ingestion is only supported then needs to be streamed to a cloud storage engine like Amazon Kinesis or Azure Event Grid 1st
  * Data can be batched of these cloud storage engines and funneled into the 3rd Party
  * Any middleware required would be the responsibility of the customer or 3rd Party to provide

<br>

## Implementation Steps

### Adobe Experience Platform

#### Schema/Datasets

1. [Configure individual profile, experience event, and multi-entity schemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) in Experience Platform, based on customer-supplied data.
1. [Create datasets](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) in Experience Platform for data to be ingested.
1. [Add data usage labels](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html) in Experience Platform to the dataset for governance.
1. [Create policies](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html) that enforce governance on destinations.

#### Profile/Identity

1. [Create any customer-specific namespaces](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Add identities to schemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Enable the schemas and datasets for Profile](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Set up merge policies](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html) for differing views of [!UICONTROL Real-time Customer Profile] (optional).
1. Create segments for Journey usage.

#### Sources/Destinations

1. [Ingest data into Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) using streaming APIs & source connectors.

### Journey Optimizer

1. Configure your Experience Platform datasource and determine what fields should be cached as part of the profileStreaming data used to initiate a customer journey must be configured within Journey Optimizer first to get an orchestration ID. This orchestration ID is then supplied to the developer to use with ingestion
1. Configure external data sources
1. Configure custom actions for 3rd party application

### Mobile Push Configuration (optional as 3rd Party may collect tokens)

1. Implement Experience Platform Mobile SDK to collect push tokens and login information to tie back to known customer profiles
1. Leverage Adobe Tags and create a mobile property with the following extension:
    * Adobe Journey Optimizer
    * Adobe Experience Platform Edge Network
    * Identity for Edge Network
    * Mobile Core
1. Ensure you have a dedicated datastream for mobile app deployments vs. web deployments
1. For more information follow the [Adobe Journey Optimizer Mobile Guide](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-journey-optimizer)

<br>

## Related Documentation

* [Experience Platform documentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Experience Platform Tags documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)
* [Experience Platform Mobile SDK documentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
* [Journey Optimizer documentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=en)
* [Journey Optimizer Product Description](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html)
