---
title: Online/Offline Audience Activation scenario
description: Online/Offline Audience Activation.
solution: Experience Platform, Real-time Customer Data Platform, Target, Audience Manager, Analytics, Experience Cloud Services, Data Collection
kt: 7086
---

# Online/Offline Audience Activation scenario

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

* For activation scenarios where audiences are shared from Experience Platform to Audience Manager, all identities included in the Real-time Customer Profile are shared to Audience Manager. The audiences from Experience Platform can be shared through Audience Manager destinations when the required destination identities are included in the Real-time Customer Profile, or where identities in the Real-time Customer Profile can be related to the required destination identities that are linked in Audience Manager.

* Audience metadata is shared from Experience Platform to Audience Manager. After 4 to 5 hours, this metadata is available in Audience Manager. Any newly realized profile audience memberships are then recorded in Audience Manager. Audience Membership realized before configuration of the Experience Platform and Audience Manager audience sharing, or before the audience metadata is synced from Experience Platform to Audience Manager, is not realized in Audience Manager. In these cases, a segment including a segment membership can be built to populate historical audience membership into Audience Manager. 


## Related Documentation

* [Real-time Customer Data Platform Product Description](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html)
* [Profile and Segmentation Guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* [Segmentation documentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html)
* [Destinations documentation](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html)

## Related Videos & Tutorials

* [Real-time Customer Data Platform overview](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/understanding-the-real-time-customer-data-platform.html)
* [Demo of Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/application-services/rtcdp/demo.html)
* [Create segments](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)