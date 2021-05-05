---
title: Triggered Messaging and Adobe Experience Platform Blueprint
description: Execute triggered messages and experiences using Adobe Experience Platform as a central hub of streaming data, customer profiles, and segmentation.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
exl-id: 97831309-f235-4418-bd52-28af815e1878
---
# Triggered Messaging and Adobe Experience Platform Blueprint

Execute triggered messages and experiences using Adobe Experience Platform as a central hub of streaming data, customer profiles, and segmentation.

## Use Cases

* Triggered messages
* Registration confirmations
* Shopping cart and application form abandons
* Location triggered messages

## Architecture

<img src="assets/triggered.svg" alt="Reference architecture for the Triggered Messaging and Adobe Experience Platform blueprint" style="border:1px solid #4a4a4a" />

## Integration Patterns

* Adobe Experience Platform -> Journey Orchestration

## Prerequisites

* Adobe Experience Platform
* Journey Orchestration

## Guardrails

### Journey Orchestration

* See link for [more details on limitations](https://experienceleague.adobe.com/docs/journeys/using/starting-with-journeys/limitations.html?lang=en#starting-with-journeys)
* Capping is available through API setup to ensure that the destination system is not saturated to the point of failure. Capping means that messages that exceed the cap are dropped completely and never sent. Throttling is still not supported.
  * max connections: Maximum number of http/s connections a destination can handle
  * max call count: Maximum number of calls to be made in the periodInMs parameter
  * periodInMs: Time in milliseconds
* Segment membership initiated journeys can operate in two modes:
  * batch segments (refreshed every 24 hours)
  * Streaming segments (<5-minute qualification)
* Batch segments: Ensure you understand the daily volume of qualified users and ensure that the destination system can handle the burst throughput per journey and across all journeys
* Streaming segments: Ensure that the initial burst of profile qualifications can be handled along with the daily streaming qualifying volume per journey and across all journeys
* Final destination must support REST API & JSON payload
* Does not support Offer Decisioning currently
* See [profile and data ingestion guardrails for Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

### Adobe Campaign Standard

* Can only support 14 tps (50k per hour) in throughput
* Segment-membership-initiated journeys are not supported
* Reaction events to transactional message open/clicks are supported within Journey Orchestration.
* Transactional messaging logs are not natively synced to Experience Platform currently, requiring a manual configuration. It is recommended to export logs at most every four hours.


## Implementation Steps

### Adobe Experience Platform

#### Schema/Datasets

1. [Configure individual profile, experience event, and multi-entity schemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) in Experience Platform, based on customer-supplied data.
1. Create Adobe Campaign schemas for broadLog, trackingLog, non-deliverable addresses, and profile preferences (optional).
1. [Create datasets](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) in Experience Platform for data to be ingested.
1. [Add data usage labels](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/classify-data-using-governance-labels.html) in Experience Platform to the dataset for governance.
1. [Create policies](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-governance/create-data-usage-policies.html) that enforce governance on destinations.

#### Profile/Identity

1. [Create any customer-specific namespaces](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Add identities to schemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html).
1. [Enable the schema and datasets for Profile](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html).
1. [Set up merge policies](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/create-merge-policies.html) for differing views of [!UICONTROL Real-time Customer Profile] (optional).
1. Create segments for Adobe Campaign usage.

#### Sources/Destinations

1. [Ingest data into Experience Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) using streaming APIs & source connectors.1. Configure [!DNL Azure] blob storage destination for use with Adobe Campaign.

#### Mobile app deployment

1. Implement Adobe Campaign SDK for Adobe Campaign Classic or Experience Platform SDK for Adobe Campaign Standard. If Experience Platform Launch is present, the recommendation is to use Adobe Campaign Classic or Adobe Campaign Standard extension with Experience Platform SDK.


### Journey Orchestration

1. Streaming data used to initiate a customer journey must be configured within Journey Orchestration first to get an orchestration ID. This orchestration ID is then supplied to the developer to use with ingestion.
1. Configure external data sources.
1. Configure custom actions.

### Adobe Campaign Standard

1. Configure messaging templates with appropriate personalization settings.
1. Configure export workflows export transactional messaging logs. Recommendation is to run at most every four hours.


## Related Documentation

* [Adobe Experience Platform documentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Journey Orchestration documentation](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=en)
* [Adobe Campaign Classic documentation](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Adobe Campaign Standard documentation](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Experience Platform Launch documentation](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK documentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
