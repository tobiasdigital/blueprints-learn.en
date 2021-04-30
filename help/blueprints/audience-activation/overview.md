---
title: Audience & Profile Activation
description: Deliver audience activated and profile centric customer experiences with Real-time Customer Data Platform​.
solution: Experience Platform, Real-time Customer Data Platform
kt: 
thumbnail:
exl-id: eeeb4325-d0e8-4fd8-86ab-0b8afdd0b69f
---

# Audience and Profile Activation

Audience and Profile activation is the key to success in a data-driven marketing world. However, many brands still focus their efforts on channel-first activation, which often delivers inconsistent reach and personalization.

With a channel-first approach, each channel acts as a silo in which personalization efforts target only the customers interacting with the brand on that channel. This approach doesn’t reflect the reality that customers interact with brands across many different touchpoints. Audience and Profile activation allows brands to connect customer interactions across multiple channels, to deliver a centralized profile and audience that can be activated to all channels.

| Blueprint | Description| Experience Cloud Applications|
|---|---|---|
| **[Anonymous Audience Activation](anonymous.md)** | <ul><li>Target audiences across web and advertising channels for anonymous and behavioral customer data.</li><li>Integrate with third-party audience data for increased personalization.</li></ul>                                                                                         | <ul><li>Adobe Audience Manager</li></ul>                                               |
| **[Online/Offline Audience Activation](online-offline.md)**        | <ul><li>Activate to known profile-based destinations, such as email providers, social networks, and advertising destinations. </li><li>Use offline attributes and events, such as offline orders, transactions, CRM, or loyalty data along with online behavior for online targeting and personalization.</li></ul> | <ul><li>Adobe Experience Platform</li><li> [!UICONTROL Real-time Customer Data Platform]</li><li>Adobe Audience Manager (optional)</li></ul> |
| **[Audience and Profile Activation to Enterprise Destinations](enterprise-destinations.md)**        | <ul><li>Replication and update of profile and audience changes to enterprise data stores for activation and reporting use cases. </li></ul><ul><li>Initiate a sales or support action to the customer through notification of a customer action from the [!UICONTROL Real-time Customer Data Platform] to enterprise systems and applications.</li></ul>| <ul><li>Adobe Experience Platform</li><li>[!UICONTROL Real-time Customer Data Platform]</li><li>Experience Platform Activation</li><li>Adobe Audience Manager (optional)</li></ul> |
| **[Customer Activity Hub](customer-activity.md)**        | <ul><li>Provide deeper consumer context to agent-supported interactions, such as support and sales experiences. Using the profile lookup into Experience Platform, agents can receive more context about the consumer, such as recent purchases, campaign interactions, propensities, audience memberships, and other attributes and insights that are stored in the real-time customer profile.</li></ul>| <ul><li>Adobe Experience Platform</li></ul> |

## Guardrails for Audience and Profile Activation Blueprints

* [Profile and Segmentation Guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)

### Guardrails for Segment Evaluation and Activation

| Segmentation Type | Frequency | Throughput | Latency (Segment Evaluation) | Latency (Segment Activation) | Activation Payload |
|-|-|-|-|-|-|
| Edge Segmentation | Edge segmentation is currently in beta and allows for valid real-time segmentation to be evaluated on the Experience Platform Edge Network for real-time, same page decisioning via Adobe Target and Adobe Journey Optimizer. |  | ~100 milliseconds | Available immediately for personalization in Adobe Target, for profile lookups in the Edge Profile, and for activation via cookie based destinations. | Audience Memberships available on the Edge for profile lookups and cookie based destinations.<br>Audience Memberships and Profile attributes are available to Adobe Target and Journey Optimizer.  |
| Streaming Segmentation | Every time a new streaming event or record is ingested into the Real-time Customer Profile and the segment definition is a valid streaming segment. <br>See the [segmentation documentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html) for guidance on streaming segment criteria | Up to 1500 events per second.  | ~ p95 < 5 minutes | Streaming Destinations: Streaming audience memberships are activated within approximately 10 minutes or micro-batched based on the requirements of the destination.<br>Scheduled Destinations: Streaming audience memberships are activated in batch based on the scheduled destination delivery time. | Streaming Destinations: Audience membership changes, identity values, and profile attributes.<br>Scheduled Destinations: Audience membership changes, identity values, and profile attributes. |
| Incremental Segmentation | Once per hour for new data that has been ingested into the Real-time Customer Profile since the last incremental or batch segment evaluation. |  |  | Streaming Destinations: Incremental audience memberships are activated within approximately 10 minutes or micro-batched based on the requirements of the destination.<br>Scheduled Destinations: Incremental audience memberships are activated in batch, based on the scheduled destination delivery time. | Streaming Destinations: Audience membership changes and identity values only.<br>Scheduled Destinations: Audience membership changes, identity values, and profile attributes. |
| Batch Segmentation | Once per day based on a predetermined system set schedule, or manually initiated ad hoc via API. |  | Approximately one hour per job for up to 10 terabytes profile store size, 2 hours per job for 10 terabytes to 100 terabytes profile store size. Batch segment job performance is dependent upon number profiles, size of profiles and number of segments being evaluated. | Streaming Destinations: Batch audience memberships are activated within approximately 10 of completion of the segmentation evaluation or micro-batched based on the requirements of the destination.<br>Scheduled Destinations: Batch audience memberships are activated based on the scheduled destination delivery time. | Streaming Destinations: Audience membership changes and identity values only.<br>Scheduled Destinations: Audience membership changes, identity values, and profile attributes. |

### Guardrails for Cross Application Audience Sharing

| Audience Application Integrations | Frequency | Throughput/Volume | Latency (Segment Evaluation) | Latency (Segment Activation) |
|-|-|-|-|-|
| Real-time Customer Data Platform to Audience Manager | Dependent on segmentation type - see above segmentation guardrails table. | Dependent on segmentation type - see above segmentation guardrails table. | Dependent on segmentation type - see above segmentation guardrails table. | Within minutes of completion of the segment evaluation.<br>Initial audience configuration sync between Real-time Customer Data Platform and Audience Manager takes approximately 4 hours.<br>Any audience memberships realized during the 4 hour period will be written to Audience Manager on the subsequent batch segmentation job as "existing" audience memberships. |
| Real-time Customer Data Platform to Ad Cloud | Note that sharing audiences from Real-time Customer Data Platform to Adobe Advertising Cloud requires Audience Manager. The same guardrails that apply for Real-time Customer Data Platform sharing to Audience Manger will apply for integration of Real-time Customer Data Platform audiences to Advertising Cloud. | - |-  | - |
| Adobe Analytics to Real-time Customer Data Platform | Not currently available | Not currently available | Not currently available | Not currently available |
| Adobe Analytics to Audience Manager |-  | By default a maximum of 75 audiences can be shared for each Adobe Analytics report suite. If an Audience Manager license is used, there is no limit on the number of audiences that can be shared between Adobe Analytics and Adobe Target or Adobe Audience Manager and Adobe Target. | - |-  |


### Guardrails for activating attributes and identities

* [!UICONTROL The Real-time Customer Data Platform] can activate audience memberships as well as attribute and identity changes that occur for profiles that are members of segments selected for activation. If your goal is to activate attributes or identities, you must define a global segment that includes all the profiles to which attribute and identity updates are sent. At that point, you can select the segment and desired attributes to activate as part of the destination configuration.
* Note that batch destinations do not support activation of attribute-only change events. Full or incremental audience memberships can be sent along with the selected attributes for activation, but you cannot activate attribute-only change events via batch destinations.  

Activating batch segments to streaming destinations

* Batch Segment Activation to Streaming Destinations is supported. Batch segment jobs place messages on the pipeline once the segment job is complete for streaming activation

Activating streaming segments to batch destinations

* Streaming segment activation to batch destinations is supported. The batch destination schedule exports profile segment memberships based on the batch destination schedule. This includes both segment memberships determined via streaming and batch methods.

Activating of experience events

* Activating raw experience events is not supported. To activate against experience events, a segment must be created with the necessary rules that include or exclude the experience event logic. This creates a segment that is defined against experience events, and the segment membership can be activated as a proxy for activating raw experience events. Also consider using [!UICONTROL Launch Server Side] to activate raw experience events collected via SDK.


## Related Blog posts

* [[!DNL Blueprints for Audience Activation in Adobe Experience Platform]](https://medium.com/adobetech/a-blueprint-for-audience-activation-in-adobe-experience-platform-b2b30fae90fd)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
