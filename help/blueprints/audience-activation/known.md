---
title: Known Customer Activation
description: Online/Offline Audience Activation.
solution: Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
exl-id: 011f4909-b208-46db-ac1c-55b3671ee48c
---
# Known Customer Activation Blueprint

Use offline attributes and events such as offline orders, transactions, CRM, or loyalty data, along with online behavior for online targeting and personalization.

Expanded identifiers with built in governance controls provide more opportunities to communicate with known customers. Activate audiences to known profile-based destinations such as email providers, social networks, and advertising destinations. 

Additional detail is provided in the [Audience and Profile Activation with Experience Cloud Applications Blueprint](platform-and-applications.md) specific to integrations between Experience Platform and Experience Cloud Applications.

## Use Cases

* Audience targeting for known audiences on social and advertising destinations.
* Online personalization with online and offline attributes.
* Activate audiences to known channels, such as email and SMS.

## Applications

* [!UICONTROL Real-time Customer Data Platform]
* Audience Manager People Based destinations can also be leveraged for people based activation to Facebook, LinkedIn, and Google Customer Match.

## Architecture

### Known Customer Activation via Real-time Customer Data Platform

<img src="assets/known_activation.svg" alt="Reference architecture for the Known Customer Activation Blueprint" style="width:90%; border:1px solid #4a4a4a" />
<br>

### Known Customer Activation via Audience Manager People Based Destinations

<img src="assets/AAM_PBD.svg" alt="Reference architecture for the Known Customer Activation Blueprint" style="width:90%; border:1px solid #4a4a4a" />
<br>

## Guardrails

[Refer to the guardrails as outlined on the Audience and Profile Activation Overview page](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/audience-activation/overview.html?lang=en#guardrails-for-audience-and-profile-activation-blueprints).

## Implementation Steps for Real-time Customer Data Platform

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

* See the [Audience and Profile Activation with Experience Cloud Applications Blueprint](platform-and-applications.md) for additional details on sharing audiences from Real-time Customer Data Platform to Audience Manager, Analytics, Target, Campaign and Journey Optimizer.

## Implementation Steps for Audience Manager People Based Destinations

* For details on implementing Audience Manager see the following [documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/implement-audience-manager.html).

* For details on implementing People Based Destinations in Audience Manager see the following [documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/faqs/faq-people-based-destinations.html).

## Related Documentation

* [[!UICONTROL Real-time Customer Data Platform] Product Description](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Profile and segmentation guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmentation documentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Destinations documentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## Related Videos & Tutorials

* [[!UICONTROL Real-time Customer Data Platform] overview](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demo of [!UICONTROL Real-time Customer Data Platform]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Create segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)
