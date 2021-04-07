---
title: Profile and Audience Activation to Enterprise Destinations Blueprint
description: Profile and Audience Activation to Enterprise Destinations
solution: Experience Platform,Real-time Customer Data Platform,Target,Audience Manager,Analytics,Experience Cloud Services,Data Collection
kt: 7086
exl-id: 32133174-eb28-44ce-ab2a-63fcb5b51cb5
---

# Profile and Audience Activation to Enterprise Destinations Blueprint

Replication and update of profile changes to enterprise data stores for activation and reporting use cases. 

Initiate a sales or support action to the customer through notification of a customer action from the Real-time Customer Data Platform to enterprise systems and applications.

## Use Cases

* Profile and Audience activation to cloud storage destinations or streaming destinations for enterprise tracking, storage, analysis, and activation of customer data and insights. 

## Applications

* Adobe Experience Platform Activation

## Architecture

<img src="assets/enterprise_destination.svg" alt="Reference architecture for the Enterprise Activation Scenario" style="border:1px solid #4a4a4a" />

## Guardrails

[Profile and Segmentation Guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

Latency and Throughput thresholds:

Streaming segmentation:

* Up to 5 minutes for streaming segmentation, at up to 1500 events per second 
* Up to 11 minutes for streaming activation

Batch segmentation:
Once per day, or manually initiated ad hoc via API 

* Approximately 1 hour per job for up to 10 TB profile store size
* Approximately 2 hours per job for 10 TB to 100 TB profile store size

## Implementation Steps

1. Create schemas for data to be ingested
1. Create datasets for data to be ingested
1. Configure the correct identities and identity namespaces on the schema to be sure that ingested data can stitch into a unified profile.
1. Enable the schemas and datasets for profile processing.
1. Configure any Sources for data ingestion
1. Author Segments in Experience Platform, to be evaluated in batch or streaming. The system automatically determines whether the segment is evaluated as batch or streaming.
1. Configure destinations for sharing of profile attributes and audience memberships to desired destinations.

## Implementation Considerations

Activation of attributes and identities

* The Real-time Customer Data Platform can activate both audience memberships as well as attribute and identity changes that occur for profiles that are members of segments that have been selected for activation. As such if the use case is to activate attributes and/or identities, a global segment must be defined that will include all the profiles for which attribute/identity updates will be sent must be defined. Once this is in place the segment and desired attributes to activate can be selected as part of the destination configuration.
* Note that batch destinations do not support activation of attribute only change events. Audience membership full or incremental can be sent along with the selected attributes for activation, but attribute only change events can not be activated via batch destinations.  

Batch Segment Activation to Streaming Destinations

* Batch Segment Activation to Streaming Destinations is supported. Batch segment jobs place messages on the pipeline once the segment job is complete for streaming activation

Streaming Segment Activation to Batch Destinations

* Streaming segment activation to batch destination is supported. The batch destination schedule will export segment memberships of the profiles based on the batch destination schedule. This includes both segment memberships determined via streaming and batch methods.

Activation of Experience Events

* Activation of raw experience events is currently not supported. To activate against experience events a segment must be created with the necessary rules that include/exclude the experience event logic to be activated against. This creates a segment that is defined against experience events - and the segment membership can be activated as a proxy for activating raw experience events. Also consider leveraging Launch Server Side for activation of raw experience events collected via SDK.

## Related Documentation

* [Real-time Customer Data Platform Product Description](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Profile and Segmentation Guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmentation documentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Destinations documentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## Related Videos & Tutorials

* [Real-time Customer Data Platform overview](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demo of Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Create segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
