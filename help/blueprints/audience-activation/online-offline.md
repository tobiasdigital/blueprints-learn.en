---
title: Online/Offline Audience Activation
description: Online/Offline Audience Activation.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
thumbnail: 
---

# Online/Offline Audience Activation scenario

Online/Offline Audience Activation.

## Use Cases

* Audience targeting for known audiences on social destinations.
* Augment web/mobile personalization efforts with granular and enriched audiences.
* Build audiences that can be exported for granular targeting and personalization in Email and Mobile messaging systems.

## Architecture

<img src="assets/onoff.svg" alt="Reference architecture for the Online/Offline Audience Activation scenario" style="border:1px solid #4a4a4a" />

## Prerequisites

* Real-time Customer Data Platform
* Profile Activation

## Guardrails

* [Profile and Segmentation Guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

## Implementation Steps

1. Configure schemas and datasets in Experience Platform.
1. Configure the correct identities and identity namespaces on the schema to be sure ingested data can stitch into a unified profile.
1. Enable the schema and datasets for Profile. 
1. Ingest data into Platform.
1. Real-time Customer Data Platform segment sharing between Experience Platform and Audience Manager must be provisioned for audiences defined in Experience Platform to be shared to Audience Manager.
1. Author Segments in Experience Platform which will be evaluated in batch or streaming. Note that the system will automatically determine if the segment will be evaluated as batch or streaming.
1. Configure Destinations for sharing of profile attributes and audience memberships out to desired destinations.

## Related Documentation

* [Real-time Customer Data Platform Product Description](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Profile and Segmentation Guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmentation documentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Destinations documentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## Related Videos & Tutorials

* [Real-time Customer Data Platform overview](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demo of Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Create segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)