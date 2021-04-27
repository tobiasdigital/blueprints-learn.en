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

### Guardrails for Segment Evaluation and Activation

| Segmentation Type | Frequency | Throughput | Latency (Segment Evaluation) | Latency (Segment Activation) | Activation Payload |
|-|-|-|-|-|-|
| Edge Segmentation | Edge segmentation is currently in beta and allows for valid real-time segmentation to be evaluated on the Experience Platform Edge Network for real-time, same page decisioning via Adobe Target and Adobe Journey Optimizer. |  | ~100 ms | Available immediately for personalization in Adobe Target, for profile lookups in the Edge Profile, and for activation via cookie based destinations. | Audience Memberships available on the Edge for profile lookups and cookie based destinations.<br>Audience Memberships and Profile attributes are available to Adobe Target and Journey Optimizer.  |
| Streaming Segmentation | Every time a new streaming event or record is ingested into the real-time customer profile and the segment definition is a valid streaming segment. <br>See the [segmentation documentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html) for guidance on streaming segment criteria  | Up to 1500 events per second.  | ~ p95 <5min | Streaming Destinations: Streaming audience memberships are activated within approximately 10 minutes or micro-batched based on the requirements of the destination.<br>Scheduled Destinations: Streaming audience memberships are activated in batch based on the scheduled destination delivery time. | Streaming Destinations: Audience membership changes, identity values, and profile attributes.<br>Scheduled Destinations: Audience membership changes, identity values, and profile attributes. |
| Incremental Segmentation | Once per hour for new data that has been ingested into the real-time customer profile since the last incremental or batch segment evaluation. |  |  | Streaming Destinations: Incremental audience memberships are activated within approximately 10 minutes or micro-batched based on the requirements of the destination.<br>Scheduled Destinations: Incremental audience memberships are activated in batch based on the scheduled destination delivery time. | Streaming Destinations: Audience membership changes and identity values only.<br>Scheduled Destinations: Audience membership changes, identity values, and profile attributes. |
| Batch Segmentation | Once per day based on a predetermined system set schedule, or manually initiated ad hoc via API. |  | Approximately one hour per job for up to 10 TB profile store size, 2 hours per job for 10 TB to 100 TB profile store size. Batch segment job performance is dependent upon number profiles, size of profiles and number of segments being evaluated. | Streaming Destinations: Batch audience memberships are activated within approximately 10 of completion of the segmentation evaluation or micro-batched based on the requirements of the destination.<br>Scheduled Destinations: Batch audience memberships are activated based on the scheduled destination delivery time. | Streaming Destinations: Audience membership changes and identity values only.<br>Scheduled Destinations: Audience membership changes, identity values, and profile attributes. |



## Implementation Steps

1. Create schemas for data to be ingested.
1. Create datasets for data to be ingested.
1. Configure the correct identities and identity namespaces on the schema to be sure that ingested data can stitch into a unified profile.
1. Enable the schemas and datasets for profile processing.
1. Configure any sources for data ingestion.
1. Author segments in Experience Platform, to be evaluated in batch or streaming. The system automatically determines whether the segment is evaluated as batch or streaming.
1. Configure destinations for sharing of profile attributes and audience memberships to desired destinations.

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
