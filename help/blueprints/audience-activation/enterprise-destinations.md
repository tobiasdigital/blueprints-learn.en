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

<img src="assets/enterprise_destination_activation.svg" alt="Reference architecture for the Enterprise Activation Scenario" style="border:1px solid #4a4a4a" />


## Guardrails

Refer to the guardrails as outlined on the Audience and Profile Activation Overview page - [LINK](overview.md)  

## Implementation Steps

1. Create schemas for data to be ingested.
1. Create datasets for data to be ingested.
1. Configure the correct identities and identity namespaces on the schema to be sure that ingested data can stitch into a unified profile.
1. Enable the schemas and datasets for profile processing.
1. Configure any sources for data ingestion.
1. Author segments in Experience Platform, to be evaluated in batch or streaming. The system automatically determines whether the segment is evaluated as batch or streaming.
1. Configure destinations for sharing of profile attributes and audience memberships to desired destinations.

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
