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
* [!UICONTROL Real-time Customer Data Platform]

## Architecture

<img src="assets/onoff.svg" alt="Reference architecture for the Online/Offline Audience Activation Blueprint" style="border:1px solid #4a4a4a" />

## Guardrails

* [Profile and Segmentation Guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

### Guardrails for Segment Evaluation and Activation

| Segmentation Type | Frequency | Throughput | Latency (Segment Evaluation) | Latency (Segment Activation) | Activation Payload |
|---|---|---|---|---|---|
| Edge Segmentation | Edge segmentation is currently in beta and allows for valid real-time segmentation to be evaluated on the Experience Platform Edge Network for real-time, same page decisioning via Adobe Target and Adobe Journey Optimizer. |  | ~100 ms | Available immediately for personalization in Adobe Target, for profile lookups in the Edge Profile, and for activation via cookie based destinations. | Audience Memberships available on the Edge for profile lookups and cookie based destinations.<br>Audience Memberships and Profile attributes are available to Adobe Target and Journey Optimizer.  |
| Streaming Segmentation | Every time a new streaming event or record is ingested into the real-time customer profile and the segment definition is a valid streaming segment. <br>See the [segmentation documentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html) for guidance on streaming segment criteria | Up to 1500 events per second.  | ~ p95 <5min | Streaming Destinations: Streaming audience memberships are activated within approximately 10 minutes or micro-batched based on the requirements of the destination.<br>Scheduled Destinations: Streaming audience memberships are activated in batch based on the scheduled destination delivery time. | Streaming Destinations: Audience membership changes, identity values, and profile attributes.<br>Scheduled Destinations: Audience membership changes, identity values, and profile attributes. |
| Incremental Segmentation | Once per hour for new data that has been ingested into the real-time customer profile since the last incremental or batch segment evaluation. |  |  | Streaming Destinations: Incremental audience memberships are activated within approximately 10 minutes or micro-batched based on the requirements of the destination.<br>Scheduled Destinations: Incremental audience memberships are activated in batch based on the scheduled destination delivery time. | Streaming Destinations: Audience membership changes and identity values only.<br>Scheduled Destinations: Audience membership changes, identity values, and profile attributes. |
| Batch Segmentation | Once per day based on a predetermined system set schedule, or manually initiated ad hoc via API. |  | Approximately one hour per job for up to 10 TB profile store size, 2 hours per job for 10 TB to 100 TB profile store size. Batch segment job performance is dependent upon number profiles, size of profiles and number of segments being evaluated. | Streaming Destinations: Batch audience memberships are activated within approximately 10 of completion of the segmentation evaluation or micro-batched based on the requirements of the destination.<br>Scheduled Destinations: Batch audience memberships are activated based on the scheduled destination delivery time. | Streaming Destinations: Audience membership changes and identity values only.<br>Scheduled Destinations: Audience membership changes, identity values, and profile attributes. |

### Guardrails for Cross Application Audience Sharing

| Audience Application Integrations | Frequency | Throughput/Volume | Latency (Segment Evaluation) | Latency (Segment Activation) |
|---|---|---|---|---|
| Real-time Customer Data Platform to Audience Manager | Dependent on segmentation type - see above segmentation guardrails table. | Dependent on segmentation type - see above segmentation guardrails table. | Dependent on segmentation type - see above segmentation guardrails table. | Within minutes of completion of the segment evaluation.<br>Initial audience configuration sync between Real-time Customer Data Platform and Audience Manager takes approximately 4 hours.<br>Any audience memberships realized during the 4 hour period will be written to Audience Manager on the subsequent batch segmentation job as "existing" audience memberships. |
| Real-time Customer Data Platform to Ad Cloud | Note that sharing audiences from Real-time Customer Data Platform to Adobe Advertising Cloud requires Audience Manager. The same guardrails that apply for Real-time Customer Data Platform sharing to Audience Manger will apply for integration of Real-time Customer Data Platform audiences to Advertising Cloud. | - |-  | - |
| Adobe Analytics to Real-time Customer Data Platform | Not currently available | Not currently available | Not currently available | Not currently available |
| Adobe Analytics to Audience Manager |-  | By default a maximum of 75 audiences can be shared for each Adobe Analytics report suite. If an Audience Manager license is used, there is no limit on the number of audiences that can be shared between Adobe Analytics and Adobe Target or Adobe Audience Manager and Adobe Target. | - |-  |






## Implementation Steps

1. Configure schemas and datasets in Experience Platform.
1. Configure the correct identities and identity namespaces on the schema to be sure that ingested data can stitch into a unified profile.
1. Enable the schema and datasets for Profile. 
1. Ingest data into Platform.
1. Provision [!UICONTROL Real-time Customer Data Platform] segment sharing between Experience Platform and Audience Manager for audiences defined in Experience Platform to be shared to Audience Manager.
1. Author Segments in Experience Platform, to be evaluated in batch or streaming. The system automatically determines whether the segment is evaluated as batch or streaming.
1. Configure destinations for sharing of profile attributes and audience memberships to desired destinations.

## Implementation Considerations

* Sharing profile data to destinations requires that you include the specific identity value used by the destination in the destination payload. Any identity that is necessary for a target destination must be ingested into Platform and configured as an identity for the [!UICONTROL Real-time Customer Profile].

* For activation scenarios where audiences are shared from Experience Platform to Audience Manager, all identities included in the [!UICONTROL Real-time Customer Profile] are shared to Audience Manager. The audiences from Experience Platform can be shared through Audience Manager destinations when the required destination identities are included in the [!UICONTROL Real-time Customer Profile], or where identities in the [!UICONTROL Real-time Customer Profile] can be related to the required destination identities that are linked in Audience Manager.

## Related Documentation

* [[!UICONTROL Real-time Customer Data Platform] Product Description](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Profile and segmentation guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmentation documentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Destinations documentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## Related Videos & Tutorials

* [[!UICONTROL Real-time Customer Data Platform] overview](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demo of [!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Create segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
