---
title: Triggered Messaging and Adobe Experience Platform
description: Execute triggered messages and experiences using Adobe Experience Platform as a central hub streaming data, customer profiles, and segmentation.
solution: Experience Platform, Campaign, Journey Orchestration
kt: 7197
thumbnail: 
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
* Capping is available via API setup to ensure that the destination system is not saturated to the point of failure. Capping means that messages that exceed the cap are dropped completely and never sent. Throttling is still not supported.
  * max connections - maximum number of http/s connections a destination can handle
  * max call count - maximum number of calls to be made in the periodInMs parameter
  * periodInMs - time in milliseconds
* Segment membership initiated journeys can operate in two modes:
  * batch segments (refreshed every 24 hrs)
  * streaming segments (<5-min qualification)
* Batch segments – ensure you understand the daily volume of qualified users and ensure that the destination system can handle the burst throughput per journey and across all journeys
* Streaming segments – ensure that the initial burst of profile qualifications can be handled along with the daily streaming qualifying volume per journey and across all journeys
* Final destination must support REST API & JSON payload
* Does not support Offer Decisioning currently
* See [profile and data ingestion guardrails for Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

### Campaign Standard

* Can only support 14 tps (50k per hour) in throughput
* Segment membership initiated journey’s are not supported
* Reaction events to transactional message open/clicks are supported within JO
* Transactional messaging logs are not natively sync’d to Experience Platform currently, requiring a manual configuration - Recommendation to export logs at most every 4 hrs


## Implementation Steps and Considerations

### Adobe Experience Platform

* Schema / Datasets
  1.  Individual profile, experience event, and multi-entity schemas are configured in Experience Platform based on customer supplied data
  1.  Campaign schemas are created for the following: broadLog / trackingLog / non-deliverable addresses / profile preferences (optional)
  1.  Dataset labels are added for governance
  1.  Policies are created for enforcing governance on destination

* Profile / Identity
  1.  Any customer-specific namespaces are created for datasets
  1.  Identities are added to schemas
  1.  Schema and datasets are enabled for profile
  1.  Merge rules are set up if differing views of real-time customer profile (optional)
  1.  Segments are created for campaign usage

* Sources / Destinations
  1.  Data is ingested into Experience Platform using streaming API’s & source connectors
  1.  Azure blob storage destination is configured for use with Campaign

* Mobile app deployment
  1.  Implement Campaign SDK for ACC or Experience Platform SDK for ACS. If Experience Platform Launch is present, the recommendation is to use ACC/ACS extension with Experience Platform SDK.

### Journey Orchestration

  1.  Streaming data used to initiate a customer journey must be configured within Journey Orchestration first to get an orchestration ID. This orchestration ID is then supplied to the developer to use with ingestion
  1.  External data sources must be configured
  1.  Custom actions must be configured

### Campaign Standard

  1.  Messaging templates must be configured with appropriate personalization settings
  1.  Export workflows must be configured to export transactional messaging logs. Recommendation is to run at most every 4 hrs


## Related Documentation

* [Adobe Experience Platform documentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Journey Orchestration documentation](https://experienceleague.adobe.com/docs/journey-orchestration.html?lang=en)
* [Campaign Classic documentation](https://experienceleague.adobe.com/docs/campaign-classic.html?lang=en)
* [Campaign Standard documentation](https://experienceleague.adobe.com/docs/campaign-standard.html?lang=en)
* [Experience Platform Launch documentation](https://experienceleague.adobe.com/docs/launch.html?lang=en)
* [Experience Platform Mobile SDK documentation](https://experienceleague.adobe.com/docs/mobile.html?lang=en)
