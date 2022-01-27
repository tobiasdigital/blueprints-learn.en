---
title: Activation with Online & Offline Data Blueprint
description: Online/Offline Audience Activation.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
---
# Activation with Online & Offline Data Blueprint

Use offline attributes and events such as offline orders, transactions, CRM, or loyalty data, along with online behavior for online targeting and personalization.

Activate audiences to known profile-based destinations such as email providers, social networks, and advertising destinations. 

The Activation with online and offline data blueprint aligns closely with the [Audience and Profile Activation with Experience Cloud Applications Blueprint](platform-and-applications.md). Additional detail is provided in the [Audience and Profile Activation with Experience Cloud Applications Blueprint](platform-and-applications.md)   specific to integrations between Experience Platform and Experience Cloud Applications.

## Use Cases

* Audience targeting for known audiences on social and advertising destinations.
* Online personalization with online and offline attributes.
* Activate audiences to known channels, such as email and SMS.

## Applications

* Adobe Experience Platform
* [!UICONTROL Real-time Customer Data Platform]

## Architecture

### Activation with Online & Offline data with destinations

<img src="assets/online_offline_activation.svg" alt="Reference architecture for the Online/Offline Audience Activation Blueprint" style="width:80%; border:1px solid #4a4a4a" />
<br>

## Guardrails

[Refer to the guardrails as outlined on the Audience and Profile Activation Overview page.](overview.md)  

## Implementation Steps

1. [Create schemas](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) for data to be ingested.
1. [Create datasets](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) for data to be ingested.
1. [Configure the correct identities and identity namespaces](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/label-ingest-and-verify-identity-data.html) on the schema to be sure that ingested data can stitch into a unified profile.
1. [Enable the schemas and datasets for profile](https://experienceleague.adobe.com/docs/platform-learn/tutorials/profiles/bring-data-into-the-real-time-customer-profile.html). 
1. [Ingest data](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2020.1.dataingestion) into Experience Platform.
1. [Provision [!UICONTROL Real-time Customer Data Platform] segment sharing](https://www.adobe.com/go/audiences) between Experience Platform and Audience Manager for audiences defined in Experience Platform to be shared to Audience Manager.
1. [Create segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) in Experience Platform. The system automatically determines whether the segment is evaluated as batch or streaming.
1. [Configure destinations](https://experienceleague.adobe.com/docs/platform-learn/tutorials/destinations/create-destinations-and-activate-data.html) for sharing of profile attributes and audience memberships to desired destinations.

## Implementation Considerations

* Sharing profile data to destinations requires that you include the specific identity value used by the destination in the destination payload. Any identity that is necessary for a target destination must be ingested into Platform and configured as an identity for the [!UICONTROL Real-time Customer Profile].

### Audience sharing from Real-time Customer Data Platform to Audience Manager

* Audience membership from RT-CDP is shared to Audience Manager in a streaming fashion as soon as segment evaluation is complete and written to the Real-time Customer profile, whether the segment evaluation occurred in batch or streaming. If the qualified profile contains the regional routing information for related profile devices then the audience membership from RTCDP is qualified in streaming fashion on the associated Audience Manager Edge. If the profiles from RTCDP do not contain regional routing information then the profile memberships are sent to the Audience Manager hub location for batch based evaluation and activation. Profiles that are eligible for Edge activation will activate within minutes of segment qualification from RTCDP, profile that do not qualify for Edge activation will qualify in the Audience Manager hub and may have a 12-24 hour timeframe for processing. 

* Regional routing information for which Audience Manager Edge the profile's related device information is stored on can be collected from the Analytics Data Connector when the Analytics data is enabled for collection to profile, or directly from the WebSDK as a separate profile record class dataset which must then be enabled for profile. 

* For activation scenarios where audiences are shared from Experience Platform to Audience Manager the following identities are shared automatically: IDFA, GAID, AdCloud, Google, ECID, EMAIL_LC_SHA256. Currently, custom namespaces are not shared. 

The audiences from Experience Platform can be shared through Audience Manager destinations when the required destination identities are included in the [!UICONTROL Real-time Customer Profile], or where identities in the [!UICONTROL Real-time Customer Profile] can be related to the required destination identities that are linked in Audience Manager.

## Related Documentation

* [[!UICONTROL Real-time Customer Data Platform] Product Description](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Profile and segmentation guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmentation documentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Destinations documentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## Related Videos & Tutorials

* [[!UICONTROL Real-time Customer Data Platform] overview](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demo of [!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Create segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
