---
title: Audience and Profile Activation to Enterprise Destinations Blueprint
description: Audience and Profile Activation to Enterprise Destinations
solution: Experience Platform,Real-time Customer Data Platform
kt: 7475
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5,None
---
# Audience and Profile Activation to Enterprise Destinations Blueprint

Share profile and audience changes and events in streaming or batch from [!UICONTROL Real-time Customer Data Platform] to enterprise data stores and applications. These profile and audience events can be used to initiate a sales or support action to the customer such as following up on an abandoned application process or webinar registration or to update enterprise applications with the latest customer attributes and intelligence from [!UICONTROL Real-time Customer Data Platform].

## Use Cases

* Profile and audience activation to cloud storage destinations, or streaming destinations for enterprise tracking, storage, analysis, and activation of customer data and insights. 

## Applications

* Adobe Experience Platform Activation

## Architecture

<img src="assets/enterprise_destination.svg" alt="Reference architecture for the Enterprise Activation Scenario" style="border:1px solid #4a4a4a" />

## Guardrails

[Profile and Segmentation Guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

Latency and throughput thresholds:

Streaming segmentation:

* Up to 5 minutes for streaming segmentation, at up to 1500 events per second 
* Up to 11 minutes for streaming activation

Batch segmentation:
Once per day, or manually initiated ad hoc via API.

* Approximately 1 hour per job for up to 10 TB profile store size
* Approximately 2 hours per job for 10 TB to 100 TB profile store size

## Implementation Steps

1. [Create schemas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/create-a-schema.html) for data to be ingested.
1. [Create datasets](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) for data to be ingested.
1. [Configure the correct identities and identity namespaces](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html) on the schema to be sure that ingested data can stitch into a unified profile.
1. [Enable the schema and datasets for Profile](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html). 
1. [Ingest data into Platform](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion).
1. [Provision [!UICONTROL Real-time Customer Data Platform] segment sharing](https://www.adobe.com/go/audiences) between Experience Platform and Audience Manager for audiences defined in Experience Platform to be shared to Audience Manager.
1. [Create segments in Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html), to be evaluated in batch or streaming. The system automatically determines whether the segment is evaluated as batch or streaming.
1. [Configure destinations](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html) for sharing of profile attributes and audience memberships to desired destinations.

## Implementation Considerations

Activating attributes and identities

* [!UICONTROL The Real-time Customer Data Platform] can activate audience memberships as well as attribute and identity changes that occur for profiles that are members of segments selected for activation. If your goal is to activate attributes or identities, you must define a global segment that includes all the profiles to which attribute and identity updates are sent. At that point, you can select the segment and desired attributes to activate as part of the destination configuration.
* Note that batch destinations do not support activation of attribute-only change events. Full or incremental audience memberships can be sent along with the selected attributes for activation, but you cannot activate attribute-only change events via batch destinations.  

Activating batch segments to streaming destinations

* Batch Segment Activation to Streaming Destinations is supported. Batch segment jobs place messages on the pipeline once the segment job is complete for streaming activation

Activating streaming segments to batch destinations

* Streaming segment activation to batch destination is supported. The batch destination schedule exports profile segment memberships based on the batch destination schedule. This includes both segment memberships determined via streaming and batch methods.

Activating of experience events

* Activating raw experience events is not supported. To activate against experience events, a segment must be created with the necessary rules that include or exclude the experience event logic. This creates a segment that is defined against experience events, and the segment membership can be activated as a proxy for activating raw experience events. Also consider using [!UICONTROL Launch Server Side] to activate raw experience events collected via SDK.

## Related Documentation

* [Destinations documentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)
* [Cloud storage destinations overview](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=en#catalog)
* [HTTP Destination](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/http-destination.html?lang=en#overview)
* [[!UICONTROL Real-time Customer Data Platform] Product Description](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Profile and segmentation guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmentation documentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)

## Related Videos & Tutorials

* [[!UICONTROL Real-time Customer Data Platform] overview](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demo of [!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Create segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
