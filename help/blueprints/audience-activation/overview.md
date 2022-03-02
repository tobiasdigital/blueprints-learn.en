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
| **[Anonymous Audience Activation](anonymous.md)** | <ul><li>Target audiences across web and advertising channels for anonymous and behavioral customer data.</li><li>Integrate with third-party audience data for increased personalization.</li></ul>|<ul><li>Adobe Audience Manager</li></ul>                                               |
| **[Known Customer Activation](known.md)**        | <ul><li>Activate to known profile-based destinations, such as email providers, social networks, and advertising destinations. </li><li>Use offline attributes and events, such as offline orders, transactions, CRM, or loyalty data along with online behavior for online targeting and personalization.</li></ul> | <ul><li>Adobe Experience Platform</li><li> [!UICONTROL Real-time Customer Data Platform]</li><li>Adobe Audience Manager (optional)</li></ul> |
| **[Activation to File and Enterprise Streaming Destinations](enterprise-destinations.md)**        | <ul><li>Activation and access of the real-time customer profile across enterprise systems and applications to power rich contextual customer experiences. </li></ul><ul><li>Initiate a sales or support experience utilizing insights and events from the real-time customer profile.</li></ul>| <ul><li>Adobe Experience Platform</li><li>[!UICONTROL Real-time Customer Data Platform]</li><li>Experience Platform Activation</li><li>Adobe Audience Manager (optional)</li></ul> |
| **[Audience and Profile Activation with Experience Cloud Applications](platform-and-applications.md)**        | <ul><li>Manage profiles and audiences in Experience Platform and share them with Experience Cloud Applications</li><li>Build and share rich customer segments and insights in Experience Platform and share them with Experience Cloud Applications</li></ul> | <ul><li>Adobe Experience Platform</li><li>[!UICONTROL Real-time Customer Data Platform]</li><li>Experience Platform Activation</li><li>Experience Cloud Applications</li></ul> |
| **[Customer Activity Hub](customer-activity.md)**        | <ul><li>Provide deeper consumer context to agent-supported interactions, such as support and sales experiences. Using the profile lookup into Experience Platform, agents can receive more context about the consumer, such as recent purchases, campaign interactions, propensities, audience memberships, and other attributes and insights that are stored in the real-time customer profile.</li></ul>| <ul><li>Adobe Experience Platform</li></ul>|

## Real-time Customer Profile Architecture

The below illustration outlines the core components of the Real-time Customer Profile of the Experience Platform.

<img src="assets/profile_architecture.jpg" alt="Reference architecture for the Real-time Customer Profile" style="border:1px solid #4a4a4a" width="90%"/>

First data sources are ingested into Experience Platform. If the data source is configured for profile processing it will feed into the Real-time Customer Profile. A single profile fragment or document is created for each data source and each primary id record that is configured for each data source. Additionally as data is ingested to the profile it is also processed by the identity service. Any record from the data sources that have more than one identity marked in the schema and with the corresponding values populated in the record will be processed as a identity relationship within the identity service. 

Note that records that have only one identity are not processed by identity service as such records have no identity links to further populate the graph with. Note as well that the identity service does not distinguish primary identities from secondary identities. It is simply processing identity relationships across identities. 

The merging of profile fragments occurs as the identity graph provides the relationships across the various source profile fragments that have been related. The merge policy determines which source fragments and which identity graph will be used as the fragments are merged. Anytime the profile is access the merging of the profile fragments occurs to ensure the most up to date combined view of the profile. Governance and policy rules ensure that only the authorized segments and attributes can be activated to the specified destinations.

## Segmentation and Destination Overview

The below illustration outlines the various segmentation methods and the various profile and audience activation patterns.

<img src="assets/segmentation_destination_overview.png" alt="Reference architecture for the Real-time Customer Profile" style="border:1px solid #4a4a4a" width="90%"/>

## Guardrails for Audience and Profile Activation Blueprints

* [Profile and Segmentation Guidelines](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en)


### Activating attributes and identities

* [!UICONTROL The Real-time Customer Data Platform] can activate audience memberships as well as attribute and identity changes that occur for profiles that are members of segments selected for activation. If your goal is to activate attributes or identities, you must define a global segment that includes all the profiles to which attribute and identity updates are sent. At that point, you can select the segment and desired attributes to activate as part of the destination configuration.
* Note that batch destinations do not support activation of attribute-only change events. Full or incremental audience memberships can be sent along with the selected attributes for activation.  

### Activating batch segments to streaming destinations

* Batch Segment Activation to Streaming Destinations is supported. As profiles qualify for audience membership from batch segment jobs, those realizations can be activated through streaming activation.

### Activating streaming segments to batch destinations

* Streaming segment activation to batch destinations is supported. The batch destination schedule exports profile segment memberships based on the batch destination schedule. This includes both segment memberships determined via streaming and batch methods.

### Activating of experience events

* Activating raw experience events is not supported. To activate against experience events, a segment must be created with the necessary rules that include or exclude the experience event logic. This creates a segment that is defined against experience events, and the segment membership can be activated as a proxy for activating raw experience events. Also consider using [!UICONTROL Launch Server Side] to activate raw experience events collected via SDK.


## Related Blog posts

* [[!DNL Blueprints for Audience Activation in Adobe Experience Platform]](https://medium.com/adobetech/a-blueprint-for-audience-activation-in-adobe-experience-platform-b2b30fae90fd)
* [[!DNL How Adobe Experience Platform Predictive Audiences improves Personalized Experiences]](https://medium.com/adobetech/how-adobe-experience-platform-predictive-audiences-improves-personalized-experiences-1f75a60cb7a3)
* [[!DNL Adobe Experience Platform Web SDK for Audience Management]](https://medium.com/adobetech/adobe-experience-platform-web-sdk-for-audience-management-751fa6d063bc)
