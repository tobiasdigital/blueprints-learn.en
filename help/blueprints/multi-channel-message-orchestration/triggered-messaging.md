---
title: Triggered Messaging and Adobe Experience Platform scenario
description: Execute triggered messages and experiences using Adobe Experience Platform as a central hub streaming data, customer profiles, and segmentation.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
---

# Triggered Messaging and Adobe Experience Platform scenario

Execute triggered messages and experiences using Adobe Experience Platform as a central hub streaming data, customer profiles, and segmentation.

## Use Cases

* Triggered messages
* Registration confirmations
* Shopping cart and application form abandons
* Location triggered messages

## Architecture

<img src="assets/triggered.svg" alt="Reference architecture for the Triggered Messaging and Adobe Experience Platform scenario" style="border:1px solid #4a4a4a" />

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

### Campaign Standard

* Can only support 14 tps (50k per hour) in throughput
* Segment-membership-initiated journeys are not supported
* Reaction events to transactional message open/clicks are supported within Journey Orchestration.
* Transactional messaging logs are not natively synced to Experience Platform currently, requiring a manual configuration. It is recommended to export logs at most every four hours.


## Implementation Steps

### Adobe Experience Platform

#### Schema / Datasets

1. Configure individual profile, experience event, and multi-entity schemas in Experience Platform based on customer-supplied data.
1. Create Campaign schemas for the following: 
  * broadLog
  * trackingLog
  * non-deliverable addresses
  * profile preferences (optional)
1. Add data usage labels to the dataset for governance.
1. Create policies to enforce governance on destinations.

#### Profile / Identity

1. Create any customer-specific namespaces.
1. Add identities to schemas.
1. Enable schemas and datasets for profile.
1. Set up merge rules for differing views of Real-time Customer Profile (optional).
1. Create segments for campaign usage.

#### Sources / Destinations

1. Ingest data into Experience Platform using streaming APIs & source connectors.
1. Configure [!DNL Azure] blob storage destination for use with Campaign.

#### Mobile app deployment

1. Implement Campaign SDK for Campaign Classic or Experience Platform SDK for Campaign Standard. If Experience Platform Launch is present, the recommendation is to use Campaign Classic/Standard extension with Experience Platform SDK.


### Journey Orchestration

1. Streaming data used to initiate a customer journey must be configured within Journey Orchestration first to get an orchestration ID. This orchestration ID is then supplied to the developer to use with ingestion.
1. Configure external data sources.
1. Configure custom actions.

### Campaign Standard

1. Configure messaging templates with appropriate personalization settings.
1. Configure export workflows export transactional messaging logs. Recommendation is to run at most every four hours.


## Related Documentation

* [Adobe Experience Platform documentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Journey Orchestration documentation](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=en)
* [Campaign Classic documentation](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Campaign Standard documentation](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Experience Platform Launch documentation](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK documentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
