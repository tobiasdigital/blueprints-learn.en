---
title: B2B Activation
description: Deliver accouunt based audiences and profile centric customer experiences with Real-time Customer Data Platform​.
solution: Experience Platform, Real-time Customer Data Platform
kt: 9311
exl-id: 
---
# B2B Audience and Profile Activation

Use account, opportunity, and lead information tied to a individual customer to create actionable b2b profiles for improved personalization and targeting across channels.

## Use Cases

* Create audiences of people for targeting and personalization across channels against B2B data including accounts, opportunities, and leads.
* Activate audiences to any Experience Platform destinations for targeting and personalization.

## Applications

* Real-time Customer Data Platform B2B Edition

## Integration Patterns

* B2B data sources (Marketo, Salesforce, etc.) -> Real-time Customer Data Platform B2B Edition -> Destinations
Various B2B data souces can be used to map account, lead, opportunity, and people data to the B2B Edition of Real-time Customer Data Platform.

## Architecture

<img src="assets/b2b-activation.svg" alt="Reference architecture for the B2B Activation Blueprint" style="width:80%; border:1px solid #4a4a4a" />
<br>

## Guardrails

Note that Marketo Engage related guardrails and implementation steps are only relevant when Marketo Engage is used as a source and/or destination.

### Multiple Instance and IMS Org Support:

The following outlines the supported patterns of mapping Experience Platform and Marketo Engage instances.

#### Marketo as a data source to Experience Platform:

* Multiple Marketo Engage instances to one Experience Platform instance is Supported. 
* Multiple Marketo Engage instances to many Experience Platform instances is not supporting. 
* One Marketo Engage instance to many Experience Platform instances is not supported.
* One Marketo Engage instance to one Experience Platform instance and multiple sandboxes is supported.  

#### Marketo as a destination to Experience Platform:

* Experience Platform to many Marketo Engage instances is supported
* Many Experience Platform instances to one Marketo Engage instance is supported

#### Experience Platform Profile and Segmentation Guardrails:

* See the profile and segmentation guardrails for Experience Platform - [Profile and Segmentation Guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)
* B2B segments which include accounts, leads, opportunities uses multi-entity relationships which result in the segment evaluation becoming batch. Streaming segmentation is supported for segments which are limited to people and events.

#### Experience Platform - Marketo Engage Source Connector: 

* Historic backfill can take up to 7 days to complete, depending on volume of data.
* Ongoing data updates and changes from Marketo are sent to Experience Platform via streaming API which can be latent up to around 5 minutes to the profile, and around 15 minutes to the data lake depending on volume.

#### Experience Platform - Marketo Destination Connector:

* Streaming segment sharing from Real-time Customer Data Platform to Marketo Engage can take up to 5 minutes.
* Batch segmentation is shared once per day based on the Experience Platform segmentation schedule. B2B segments which include accounts, leads, opportunities uses multi-entity relationships which result in the segment becoming batch.

#### Marketo Engage Guardrails:

* Contacts and leads must be ingested and defined directly in Marketo Engage for the Real-time Customer Data Platform audience to match to a Marketo Engage contact and lead. 

#### Destination Guardrails

* Please refer to the destination documentation for specific guidance on the destinations. [Destination Guidelines](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)


## Implementation Steps

For guidance on how to implement and configure the B2B Edition of the Real-time Customer Data Platform please see the B2B Edition of the Real-time Customer Data Platform Documentation. [B2B Edition of Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=en)

Two possible implementation patters exist. Both the ability to ingest B2B data and profiles from Marketo Engage or the ability to ingest B2B data from other CRM data sources.

## Implementation Considerations

Guidance on key considerations and configurations of the blueprint.

* CRM Integration with and without Marketo:
If the implementation will be using Marketo Engage as a source and Marketo Engage is connected to the CRM, then use the Marketo source connector in Experience Platform to ingest the CRM data into Experience Platform. Use the Experience Platform source connector if additional tables need to be ingested. If the implementation will not be using Marketo Engage as a source connect the CRM source directly to AEP using the CRM source Experience Platform connector. 
* Lead initiation and nurturing out of the B2B Edition of Real-time Customer Data Platform alone is not recommended. The use of a lead nurturing tool(such as Marketo Engage) is recommended for this use case.
* The Marketo Engage destination connector for AEP which pushes audiences to Marketo Engage for activation, only pushes email addresses and ECIDs. It does not create a new lead if the contact does not already exist, hence it is required to ingest the profile and lead data into Marketo Engage.

## Related Documentation

* [B2B Edition of Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/b2b-overview.html?lang=en)
* [Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform.html?lang=en)
* [Marketo Engage](https://experienceleague.adobe.com/docs/marketo/using/home.html?lang=en) 
* [Adobe Experience Platform - Marketo Source Connector](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/marketo/marketo.html?lang=en)
* [Adobe Experience Platform – Marketo Destination Connector](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) 