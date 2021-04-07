---
title: Online/Offline Audience Activation Blueprint
description: Online/Offline Audience Activation.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
---
# Online/Offline Audience Activation Blueprint

Use offline attributes and events such as offline orders, transactions, CRM, or loyalty data, along with online behavior for online targeting and personalization.

Activate audiences to known profile-based destinations such as email providers, social networks, and advertising destinations. 

## Use Cases

* Audience targeting for known audiences on social and advertising destinations.
* Online personalization with online and offline attributes.
* Activate audiences to known channels, such as email and SMS.

## Applications

* Adobe Experience Platform
* Real-time Customer Data Platform

## Architecture

<img src="assets/onoff.svg" alt="Reference architecture for the Online/Offline Audience Activation scenario" style="border:1px solid #4a4a4a" />

## Guardrails

* [Profile and Segmentation Guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* Batch segment jobs run once per day based on the pre-determined schedule. Segment export jobs are then run prior to the scheduled destination delivery. Note that batch segment jobs and destination delivery jobs run separately. Batch segment jobs and export job performance is dependent upon number of profiles, size of profiles and number of segments being evaluated.
* Streaming segment jobs are evaluated in minutes of streaming data arriving to profile and immediately write the segment membership to the profile and send a event for applications to subscribe to.
* Streaming segment membership is acted upon immediately for streaming destinations and is delivered in either single segment membership events or a micro-batch of multiple profile events dependent upon the ingestion patterns of the destination. Scheduled destinations will initiate a segment export job from profile prior to delivery, for any segments evaluated in streaming that are delivered via scheduled batch segment delivery.
* For sharing RTCDP segment membership to Audience Manager, this happens within minutes for streaming segments and within minutes upon completion of the batch segment evaluation for batch segmentation.
* Segments shared from Experience Platform to Audience Manager are shared within minutes of segment realization - whether via the streaming or batch evaluation method. There is an initial segment configuration sync between AEP and AAM once the segment is initially created, after ~4 hours the AEP segment memberships can begin to be realized in AAM profiles. Audience Membership realized before configuration of the Experience Platform and Audience Manager audience sharing or before the audience meta-data is synced from Experience Platform to Audience Manager will not be realized in Audience Manager until the following segment job where "existing" segment memberships are shared.
* Batch or streaming destination jobs from batch segments jobs can share profile attribute updates as well as segment memberships.
* Streaming segmentation jobs to streaming destinations share segment membership updates only. 

## Implementation Steps

1. Configure schemas and datasets in Experience Platform.
1. Configure the correct identities and identity namespaces on the schema to be sure that ingested data can stitch into a unified profile.
1. Enable the schema and datasets for Profile. 
1. Ingest data into Platform.
1. Provision Real-time Customer Data Platform segment sharing between Experience Platform and Audience Manager for audiences defined in Experience Platform to be shared to Audience Manager.
1. Author Segments in Experience Platform, to be evaluated in batch or streaming. The system automatically determines whether the segment is evaluated as batch or streaming.
1. Configure destinations for sharing of profile attributes and audience memberships to desired destinations.

## Implementation Considerations

* Sharing profile data to destinations requires that you include the specific identity value used by the destination in the destination payload. Any identity that is necessary for a target destination must be ingested into Platform and configured as an identity for the Real-time Customer Profile.

* For activation scenarios where audiences are shared from Experience Platform to Audience Manager, all identities included in the [!UICONTROL Real-time Customer Profile] are shared to Audience Manager. The audiences from Experience Platform can be shared through Audience Manager destinations when the required destination identities are included in the [!UICONTROL Real-time Customer Profile], or where identities in the [!UICONTROL Real-time Customer Profile] can be related to the required destination identities that are linked in Audience Manager.

## Related Documentation

* [Real-time Customer Data Platform Product Description](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Profile and Segmentation Guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmentation documentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Destinations documentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## Related Videos & Tutorials

* [Real-time Customer Data Platform overview](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demo of Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Create segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
